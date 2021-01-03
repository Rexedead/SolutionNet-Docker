# docker run -d --name sapp -p 80:5000 -v "./":/app tiangolo/uwsgi-nginx-flask
# FROM tiangolo/uwsgi-nginx-flask:python3.8

FROM tiangolo/uwsgi-nginx-flask
ENV STATIC_URL /app/static
COPY . /app/
RUN apt update
RUN pip install -r ./requirements.txt
CMD [ "python", "spacechem.py" ]