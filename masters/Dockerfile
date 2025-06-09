# Python image
FROM python:3.11-slim

# Workdir
WORKDIR /app

# Sistemdə lazım olacaq paketlər
RUN apt-get update && apt-get install -y gcc

# Layihə fayllarını konteynerə kopyala
COPY . .

# Pipenv quraşdır
RUN pip install pipenv

# Virtual env və dependensiləri quraşdır
RUN PIPENV_VENV_IN_PROJECT=1 pipenv install --deploy --ignore-pipfile

# Migrate və collectstatic (əgər lazımdırsa)
RUN .venv/bin/python manage.py collectstatic --noinput || true
RUN .venv/bin/python manage.py migrate || true

# Portu aç
EXPOSE 8000

# Başlatma komandası
CMD [".venv/bin/gunicorn", "masters.wsgi:application", "--bind", "0.0.0.0:8000"]
