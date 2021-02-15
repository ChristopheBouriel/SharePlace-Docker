# About this repo :
That was an existing application I decided to dockerize to learn how to use this tool and train myself.  
It has already been deployed using cloud services and you can find the frontend and backend in my repositories. 
You can also read more about this project in my portfolio :  
https://portfolio-christophe-bouriel.netlify.app  
The link to find it on Internet is https://shareplace4u.netlify.app

Now, to get the whole app running in containers :

1. Clone this repository

git clone https://github.com/ChristopheBouriel/SharePlace-Docker.git

If you want the building to be faster and don't feel the need to get a phpMyAdmin connected, execute the 	following instructions :  
	* open the docker-compose.yml  
	* remove this part of the file :
		phpmyadmin:
    		  depends_on:
		    - mysql
    		  image: phpmyadmin/phpmyadmin
    		  environment:
      		    PMA_HOST: mysql
		  links:
 		    - mysql:mysql
  		  ports:
   		    - 8080:80
    		  restart: always  
	* save the file

If you want it to be even faster, don't build Angular inside the container and use the dist folder (why I 	let it in this repo). To do that :  
	* enter the client folder and open the Dockerfile  
	* suppress everything and replace it with the following lines :
		FROM nginx:1.17.1-alpine
		COPY nginx.conf /etc/nginx/nginx.conf
		COPY dist/Front-end /usr/share/nginx/html
		EXPOSE 80  
	* save the file  
	* edit the .dockerignore file and delete "client"  
	* save the file  

2. In your terminal, enter the root folder of the project and just type the command :
docker-compose up -d

If you see an error at step 7/10 which stop the process, simply type again the same command : 
	docker-compose up -d
	That will start again where the process was at, and terminate it (likely a problem of timeout because my 	machine is not really powerfull... but maybe yours too)

3. Then, just go to localhost:4200 in your browser and try the app.

	If you don't want to create a profile, you can log in with this one:  
			Username --> Userix  
			Password --> evaluatapp  
	If you want to try the moderator profil with its specific functionalities:  
			Username --> Moderator  
			Password --> moderate  

	If you decided to install the phpMyAdmin, you can find the panel at localhost:8080 in your browser (the DB 	name is "sampledb")

4. In the end, if you want to clear up everything* after testing, type the command :  
	docker-compose down --rmi all --volume  
	Note that you still have to remove node and nginx images manually.
