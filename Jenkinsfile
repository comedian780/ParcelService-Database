node {
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/sabertoothx6/ParcelService-Database.git'
   }
   stage('Build Docker Image')
   {
      if(isUnix())
      {
          //Create Variable that holds the info if docker image exists
          IMAGE_EXISTS = sh(
          script: "docker images -q parcelservice-database",
          returnStatus : true)
          //Remove the previous build image if it was build before
          if(IMAGE_EXISTS!="")
          {
              sh "docker rmi -f parcelservice-database"
          }
          //Build new container with image parcelservice-database
          sh "docker build -t asset.allgaeu-parcel-service.de:5000/parcelservice-database:${currentBuild.number} ."
          sh "docker tag asset.allgaeu-parcel-service.de:5000/parcelservice-database:${currentBuild.number} asset.allgaeu-parcel-service.de:5000/parcelservice-database:latest"
      }
      else
      {
          //TODO other than unix
      }

   }
   stage('Deploy Image to Asset-Server')
   {
      sh "docker push asset.allgaeu-parcel-service.de:5000/parcelservice-database:${currentBuild.number}"
      sh "docker push asset.allgaeu-parcel-service.de:5000/parcelservice-database:latest"
      //sh "docker save parcelservice-database:${currentBuild.number} > database.${currentBuild.number}.tar"
      //sh "sshpass -p 'vagrant' scp -o StrictHostKeyChecking=no database.${currentBuild.number}.tar vagrant@192.168.56.100:/home/vagrant/images"
   }
   /*stage('Run ParcelService-Server')
   {//TODO Befehl ändern
      sh "docker run -d -p 8083:80 --name=rest parcelservice-database"
   }*/
}
