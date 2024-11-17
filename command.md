chmod +x ./entrypoint.sh
http:/0.0.0.0:8000/
docker-compose up -d --build
python manage.py startapp taskapp
docker exec -it django /bin/sh