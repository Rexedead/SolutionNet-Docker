# SolutionNet (spacechem.net)

This is the source code for [SolutionNet](http://spacechem.net), a site for sharing and comparing solutions for the game [SpaceChem](http://www.spacechemthegame.com).

## Disclaimers/Warnings

I have not actively maintained SolutionNet in years. I am willing to merge in pull requests with fixes/enhancements if they are implemented in a reasonable way and have been tested.

All image files in the `static/` directory except the SolutionNet logo were extracted from the game's assets and are the property of [Zachtronics Industries](http://www.zachtronics.com/).

SolutionNet was one of my first projects using multiple technologies, including Python, Flask, and SQLAlchemy. There are many things in it that I would do differently now that I have more experience, so I apologize for the messiness/ugliness/etc.

## Getting a dev instance running

The most basic need will be to remove the `.example` extension from the `spacechem.cfg.example` and `spacechem.wsgi.example`, and edit them to contain appropriate values for your environment. See [the Flask documentation](http://flask.pocoo.org/docs/) for information about how to set it up, if necessary.

SolutionNet itself uses a PostgreSQL database, but it should be possible to use MySQL, SQLite, or other databases supported by SQLAlchemy as well. An Amazon Web Services account is not necessary unless you want to send the registration emails using SES.

Versions of relevant packages being used on SolutionNet at 2020.03 (other versions may not work without requiring modifications):

* boto - 2.49.0
* Flask - 1.1.1
* Flask-SQLAlchemy - 2.4.1
* Flask-Uploads - 0.2.1
* Flask-WTF - 0.14.3
* bcrypt - 3.1.7
* SQLAlchemy - 1.3.15
* Werkzeug - 0.16 (!)
* WTForms - 2.2.1

## Sample setup steps with ubuntu vivid, postgres, uwsgi and nginx
Clone the SolutionNet repo
Edit spacechem.cfg.example as follows:

  - **SECRET_KEY** - generate a secret key for session encryption and paste it here
  - **AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, FROM_EMAIL_ADDRESS,AWS_REGION** - these can be left as they are. If you want the system to send out a registration email via Amazon SES, fill these in
  - **SRV_NAME** - host header of the site for nginx to use
  - **GA_ID** - Google Analytics tracking id

```
Then:
docker-compose up -d

# Container doesnt include:

## Configure daily statistics update
echo "0 0 * * * python /home/spacechem/SolutionNet/update_scores.py" > cronline
sudo -u root crontab cronline
rm cronline

## Populate the current high scores
python /app/update_scores.py
## If scores servers down, you can use last collected stats