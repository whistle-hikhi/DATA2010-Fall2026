# Week 07 — Reproducibility with Docker

## Overview
In [Week 3](../Week_03/Week_03.md) you fixed random seeds and recorded package versions. Your analysis can still break on another computer, because the OS, the Python/R version or the system libraries may be different. **Docker** fixes this by bundling your code *and* the environment it runs in into an **image**. A **container** is a running copy of that image. Anyone with Docker can run it with one command and get the same result.

This week you'll put your Week 3 project R into Docker containers.

## Setup
- Install [Docker Desktop](https://www.docker.com/products/docker-desktop/), then check that it works:
  ```bash
  docker --version
  docker run --rm hello-world
  ```
- Can't install Docker? Use [GitHub Codespaces](https://github.com/features/codespaces), which has Docker preinstalled, or [Play with Docker](https://labs.play-with-docker.com/).

## Submission Instructions (Only need submit in R but I will show you some in Python)
- Submit one folder `week07_yourname/` (zipped) on Canvas with this structure:
  ```
  week07_yourname/
  ├── data/
  ├── scripts/
  │   ├── analysis.py
  │   └── analysis.R
  ├── outputs/            # produced by the containers
  ├── requirements.txt
  ├── Dockerfile.python
  ├── Dockerfile.r
  └── README.md
  ```

---

## Task 1 — Your First Container
Run Python and R without installing them:
```bash
docker run --rm python:3.12-slim python --version
docker run --rm rocker/r-ver:4.4.1 R --version
```
In your README, answer in 1–2 sentences: what does the **tag** (`3.12-slim`, `4.4.1`) do, and why is using `latest` bad for reproducibility?

## Task 2 — Write the Dockerfiles
Change your Week 3 scripts so they read from `data/` and write their results to `outputs/`. Then use these starter files and fill in your own packages and file names.

**`Dockerfile.python`** (pin exact versions in `requirements.txt`, e.g. `pandas==2.2.3`):
```dockerfile
FROM python:3.12-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY scripts/ scripts/
COPY data/ data/
CMD ["python", "scripts/analysis.py"]
```

**`Dockerfile.r`** (versioned `rocker/r-ver` images install packages from a fixed-date CRAN snapshot):
```dockerfile
FROM rocker/r-ver:4.4.1
WORKDIR /app
RUN install2.r --error dplyr readr
COPY scripts/ scripts/
COPY data/ data/
CMD ["Rscript", "scripts/analysis.R"]
```

Build both images:
```bash
docker build -f Dockerfile.python -t week07-py .
docker build -f Dockerfile.r -t week07-r .
```

## Task 3 — Run and Get Your Outputs Out
Files written inside a container are lost when the container is removed. Mount your local `outputs/` folder into the container so the results are saved on your machine:
```bash
docker run --rm -v "$(pwd)/outputs:/app/outputs" week07-py
docker run --rm -v "$(pwd)/outputs:/app/outputs" week07-r
```
(On Windows PowerShell, use `${PWD}` instead of `$(pwd)`.) Check that your output files now appear in `outputs/`.

## Task 4 — Prove It and Document It
1. Delete everything in `outputs/`, rebuild with `docker build --no-cache ...`, run again, and confirm that the outputs are the same as before.
2. Add a **"Run with Docker"** section to your README with the exact commands needed to go from a fresh clone to the results.
3. In 3–4 sentences, explain: what does Docker pin that `requirements.txt`/`sessionInfo()` alone does not? What can **still** make results differ? (Think about unpinned packages, the `latest` tag, missing seeds and hardware.)

---

## Notes
- Add a `.dockerignore` file (like `.gitignore`) listing `outputs/` and other large files that shouldn't be copied into the image.
- Docker caches each line of the Dockerfile as a layer. That's why dependencies are installed *before* the scripts are copied: editing your script won't trigger a reinstall of every package.
- Rule of thumb: if a classmate can run your two `docker run` commands and get your exact outputs, you've succeeded this week.
