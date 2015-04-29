Backup Firebase data to AWS S3
==============================

Detailed blog post here: http://www.seanmeadows.com/2014/03/firebase-continuous-backup/

Using python, you can automatically (with cron or heroku scheduler) backup all
your Firebase data and store it safely on AWS S3.

The result is a new .json file in your S3 bucket whenever you run this script.

Install
-------

    virtualenv -p python2.7 --distribute venv
    source venv/bin/activate
    pip install -r requirements.txt

Run
---

Set the necessary environment variables. Then run:

    python backup-firebase.py

Heroku setup
---------------------

    heroku create yourapp-backup
    heroku addons:add scheduler
    heroku config:set\
        FIREBASE_URL=https://yourapp.firebaseio.com/\
        FIREBASE_SECRET=firebaseSecret\
        FIREBASE_USERNAME=username\
        AWS_ACCESS_KEY_ID=awsAccessID\
        AWS_SECRET_ACCESS_KEY=awsSecret\
        AWS_BUCKET=awsBucketName
    git push heroku master
    
In the Heroku dashboard, configure scheduler to run `python backup-firebase.py` as often as you desire.
