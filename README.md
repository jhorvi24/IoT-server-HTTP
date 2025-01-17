# Servidor web para IoT en AWS EC2

Se va a implementar un servidor web que reciba datos de un ESP32 y los almacene en un archivo CSV

![Flask](https://img.shields.io/badge/flask-%23000.svg?style=for-the-badge&logo=flask&logoColor=white) ![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) ![AWS](https://img.shields.io/badge/Amazon_AWS-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![arduino](https://img.shields.io/badge/Arduino-00979D?style=for-the-badge&logo=Arduino&logoColor=white)
![espressiff](https://img.shields.io/badge/espressif-E7352C?style=for-the-badge&logo=espressif&logoColor=white)

<hr>

Vamos al servicio AWS EC2. 

   Creamos un grupo de seguridad con las siguientes configuraciones.      
      
   - Name: IoT-server-SG
   - Inboud rules:
      - Type: Custom TCP
      - Port Range: 5000
      - Source: 0.0.0.0/0
      - Type: ssh
      - Port Range: 22
      - Source: myIP        
      
   Creamos una instancia EC2 donde vamos a configurar el servidor IoT utilizando el framework flask de python. La instancia tiene las siguientes configuraciones:
   
   - AMI: *Amazon Linux 2023*
   - Instance Type: *t2.micro*
   - Key Pair: associate a key pair
   - Network settings:
     - VPC
     - Public Subnet: enable *Public IP*
     - Security Group: IoT-server-SG
     - Advanced details:

     - User data: *copy the next following lines to the user data*
          
                    #!/bin/bash
                    sudo dnf install -y python3.9-pip
                    pip install virtualenv           
                    sudo dnf install -y git           
                    pip install flask           
                    git clone https://github.com/jhorvi24/IoT-server-HTTP.git
            
      - Una vez que la instancia se está ejecutando puedes conectarte a través de SSH, comprobar que las librerías se han instalado y que el repositorio de GitHub se ha clonado.  
                   
      - Para correr el servidor IoT debes ubicarte en la carpeta que se ha clonado donde está el archivo server.py. Verifica que el grupo de seguridad tiene los respectivos puertos  abiertos y ejecuta el siguiente comando para correr el servidor IoT.
               
               python app.py 
               
  
      
      - El archivo con extensión .ino lo debes correr en el ESP32 
      - Verifica que el servidor IoT está recibiendo los datos y los está almacenando un archivo csv. 
