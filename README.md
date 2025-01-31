Requirements
Before you start, make sure you have the following installed on your machine:
1. Python 3.9 for the backend (Django)
2. Node.js for the frontend (React)
3. Docker for containerizing the application

Installation Steps
1. Clone the Repository
First, download the project to your local machine by running the following command:
git clone https://github.com/suju12312/Django-notes-app.git
This will create a folder called Django-notes-app with all the necessary files.
2. Build the Application with Docker
Next, build the Docker image for the app. This will create a container image that contains both the frontend and backend of the app.
docker build -t notes-app .
This command uses the Dockerfile to build the image and tag it as notes-app.
3. Run the Application
After building the Docker image, run the app using the following command:
docker run -d -p 8000:8000 notes-app:latest

4. Setting Up Nginx as a Reverse Proxy
To make this app available on the web, you can use Nginx as a reverse proxy. This allows you to serve the app using a web server.
Install Nginx (for reverse proxy): 1. sudo apt-get update  2. sudo apt install nginx
This will install Nginx, which is a popular web server. Once it’s installed, you can configure it to forward traffic to the Docker container running your app.
Configure Nginx
Open the Nginx configuration file to set it up as a reverse proxy:
sudo nano /etc/nginx/sites-available/default
In the server block, update the configuration to forward requests to the Django application running on port 8000:
server {
    listen 80;
    server_name localhost;

    location / {
        proxy_pass http://localhost:8000;  # Pointing to the Docker container running the Django app
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
After saving the file, restart Nginx to apply the changes:
sudo systemctl restart nginx
Now, your app should be available on port 80 (the default web port) instead of port 8000. You can access it by visiting http://localhost or your server’s IP address.

Feel free to reach out if you run into any issues or need further help! 😊
