# fun

IN THIS PROJECT I AM TRYING TO COPY AN INDUSTRIAL USE CASE IN WHICH AS SOON AS THE DEVELOPER WHO IS WORKING ON MASTER BRANCH
COMMITS HIS FILES ARE AUTOMATICALLY PUSHED TO GITHUB .FROM HERE JENKINS COMES INTO PLAY AND AUTOMATICALLY LAUNCHES A DOCKER CONTAINER
IN WHICH THE WEBSITE IS HOSTED AND CAN BE SEEN BY CLIENTS IMMEDIATELY.
THIS SCENARIO RESEMBLES TO SCENARIO OF PRODUCTION TEAM IN A INDUSTRY WHO WORK ON MASTER BRANCH AND ANY CHANGES MADE BY THEM ARE
IMMEDIATELY VISIBLE TO CUTOMER 

ANOTHER DEVELOPER WORKING ON DEV1 BRANCH CAN WORK SIMULTANEOUSLY ON SAME FILE AND WHEN HIS CHANGES ARE APPROVED BY QUALITY ASSRANCE TEAM IT COULD BE MERGED TO MASTER BRANCHED AND DEPLOYED IMMEDIATELY 

FOR DOING SOLVING THIS AWSOME USE CASE
GO TO git bash:
         -> cd desktop
         -> mkdir myproject
         ->cd myproject
         ->git init
         ->cat > index.html
         ->HELLO WORLD
          In order to create hooks so that as soon as you commit your files get automatically pushed to git hub:
                     notepad .git/hooks/post-commit
                          In the post-commit type:
                               #!bin/bash
                               git push --all
          ->git add  
          ->git commit . -m "commit by master"
          ->git checkout -b dev1
          ->cat >> index.html
          HELLO INDIA
          ->git commit . -m "commit by dev1"
          ->cat >> index.html
          HELLO VARANASI HELLO RADIO MIRCHI
          ->git commit . -m "commit by dev1"
NOW WHEN YOU GO TO YOUR GIT HUB REPOSITORY YOU CAN SEE index.html WHERE IF YOU CHANGE BRANCHES FROM MASTER TO DEV1 YOU WILL SEE THE
COMMITED CHANGES ACCORDINGLY


NOW GO TO REDHAT
      ->mkdir /1
      ->mkdir /2
      ->systemctl start jenkins
      ->systemctl start docker
      
TO LAUNCH AN OS WHICH RESEMLES THE ONE BEING LAUNCHED FROM PRODUCTION AREA  GO TO YOUR JENKINS
     CLICK ON NEW ITEM:
          GIVE ITEM NAME: t11
          CHOOSE FREE STYLE PROJECT
          CLICK ON OK.
         
         IN SOURCE CODE MANAGEMENT:
               SELECT GIT
               ENTER THE REPOSITORY URL OF GITHUB
               IN BRANCH SPECIFIER WRITE */master
         IN BUILD TRIGGERS:
               SELECT POLL SCM
                    IN THE BOX type * * * * *
         IN BUILD WRITE THE FOLLOWING COMMANDS:
                     sudo cp -v -r -f * /1
                     if sudo docker ps | grep os1
                     then
                     echo "already running"
                     else
                     sudo docker run -dit -p 8000:80 -v /1:/usr/local/apache2/htdocs/ --name os1 httpd:latest
                     fi
         CLICK ON APPLY AND SAVE 
   GO TO BROWSER TYPE YOUR BASE OS IP:PORT NO which you have exposed for this container
NOW ANY CHANGES THAT YOU MAKE IN MASTER BRANCH THROUGH GIT IS IMMEDIATELY VISIBLE TO CLIENT (MASTER HERE RESEMBLES PRODUCTION AREA)

TO LAUNCH AN OS WHICH RESEMLES THE ONE BEING LAUNCHED FROM TESTING AREA  GO TO YOUR JENKINS
     CLICK ON NEW ITEM:
          GIVE ITEM NAME: t12
          CHOOSE FREE STYLE PROJECT
          CLICK ON OK.
         
         IN SOURCE CODE MANAGEMENT:
               SELECT GIT
               ENTER THE REPOSITORY URL OF GITHUB
               IN BRANCH SPECIFIER WRITE */dev1
         IN BUILD TRIGGERS:
               SELECT POLL SCM
                    IN THE BOX type * * * * *
         IN BUILD WRITE THE FOLLOWING COMMANDS:
                     sudo cp -v -r -f * /2
                     if sudo docker ps | grep os2
                     then
                     echo "already running"
                     else
                     sudo docker run -dit -p 8001:80 -v /2:/usr/local/apache2/htdocs/ --name os2 httpd:latest
                     fi
         CLICK ON APPLY AND SAVE 
  GO TO BROWSER TYPE YOUR BASE OS IP:PORT NO which you have exposed for this container         
NOW ANY CHANGES THAT YOU MAKE IN DEV1 BRANCH THROUGH GIT IS VISIBLE AT THIS IP:PORT NO

TILL NOW WHATEVER CHANGES YOU MAKE IN MASTER OR DEV1 BRANCH IS VISIBLE AT THE DIFFERNT IP SPECIFIED EARLIER

NOW WHEN THE QUALITY ASSURANCE TEAM FEELS DEV1 HAS WORKED SUCCESFULLY HE CAN BE MERGED NOW TO MASTER BRANCH BEACAUSE ITS THE MASTER BRANCH ONLY WHOSE DATA IS VISIBLE TO CLIENT FROM PRODUCTION AREA

  TO DO THIS GO TO JENKINS:
                   GIVE ITEM NAME: t13
                   CHOOSE FREE STYLE PROJECT
                   CLICK ON OK.
                   
                   IN SOURCE CODE MANAGEMENT:
                        SELECT GIT
                        ENTER THE REPOSITORY URL OF GITHUB
                        give the credentials githubusername and password
                      IN ADDITIONAL BEHAVIOUR
                           CHOOSE MERGE BEFORE BUILD
                               Name of repository : origin
                               Branch to merge to : DEV1
                  IN BUILD TRIGGERS
                       CHOOSE Trigger builds remotely (e.g., from scripts):
                                 WRITE TT1
                  IN POST BUILD ACTIONS:
                        CHOOSE GIT PUBLISHER
                             Push Only If Build Succeeds: tick this	
                              Merge Results:tick this
                              BRANCHES: 
                                   Branch to push: master
                                   Target remote name: origin
                 
                 
                 CLICK ON APPLY AND SAVE
                 
BOOM !!! your dev1 and master branch have been merged successfully and you can now see all commits on both the IPs.
           
      
      
      
      
      
     
      
      
          
          
          
          
                              
          
