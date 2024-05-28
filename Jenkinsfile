node {

   stage('clone repo') {
        git 'https://github.com/moulitechhub/maven-web-app.git'
    }


    stage ('Maven Build'){
        def mavenHome = tool name: "Maven-3.9.6", type: "maven"
        def mavenCMD = "${mavenHome}/bin/mvn"
        sh "${mavenCMD} clean package"
    }


    stage('SonarQube analysis') {
    		withSonarQubeEnv('Sonar') {
    		def mavenHome = tool name: "Maven-3.9.6", type: "maven"
    		def mavenCMD = "${mavenHome}/bin/mvn"
    		sh "${mavenCMD} sonar:sonar"
    	}
    }

    stage ('Nexus Upload'){
        nexusArtifactUploader artifacts: [[artifactId: 'moulitechhub-web-app', classifier: '', file: 'target/moulitechhub-web-app.war', type: 'war']], credentialsId: 'nexus-creds', groupId: 'in.moulitechhub', nexusUrl: '54.146.62.46:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'moulitechhub-snapshot-repository', version: '3.0-SNAPSHOT'
    }
}
