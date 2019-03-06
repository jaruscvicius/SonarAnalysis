# SonarAnalysis

### Instructions:

**1.** Clone this repository in a directory of your preference

`git clone https://github.com/jaruscvicius/SonarAnalysis`

**2.** Go into the directory and run the following command to build the containers of SonarQube

`make build`

**3.** Access the url [localhost:9000](http://localhost:9000) to see if the container is up. Case yes, log in with the following credentials

	Login: admin
	Password: admin

**4.** Copy the file *sonar-project.properties* to the root directory of your project and edit with the properties of your choice. The file should be like

	# Required metadata
	sonar.projectKey=<the-key-of-your-project>
	sonar.projectName=<the-name-of-your-project>
	sonar.projectVersion=1.0
	
	# Path to the parent source code directory.
	# Path is relative to the sonar-project.properties file. Replace "\" by "/" on Windows.
	# Since SonarQube 4.2, this property is optional if sonar.modules is set. 
	# If not set, SonarQube starts looking for source code from the directory containing 
	# the sonar-project.properties file.
	sonar.sources=<source-of-your-code>
	
	# Encoding of the source code
	sonar.sourceEncoding=UTF-8

**5.** Download [SonarQube Runner](http://repo1.maven.org/maven2/org/codehaus/sonar/runner/sonar-runner-dist/2.4/sonar-runner-dist-2.4.zip) and unzip the downloaded file into the */opt/* directory

`sudo unzip ~/Dowloads/sonar-runner-dist-2.4.zip -d /opt/`

**6.** Update the global settings by editing */opt/sonar-runner-2.4/conf/sonar-runner.properties* file. The result should be as below

	#Configure here general information about the environment, such as SonarQube DB details for example
	#No information about specific project should appear here

	#----- Default SonarQube server
	sonar.host.url=http://localhost:9000

	#----- PostgreSQL
	#sonar.jdbc.url=jdbc:postgresql://localhost/sonar

	#----- MySQL
	#sonar.jdbc.url=jdbc:mysql://localhost:3306/sonar?useUnicode=true&amp;characterEncoding=utf8

	#----- Oracle
	#sonar.jdbc.url=jdbc:oracle:thin:@localhost/XE

	#----- Microsoft SQLServer
	#sonar.jdbc.url=jdbc:jtds:sqlserver://localhost/sonar;SelectMethod=Cursor

	#----- Global database settings
	sonar.jdbc.username=sonar
	sonar.jdbc.password=sonar

	#----- Default source code encoding
	sonar.sourceEncoding=UTF-8

	#----- Security (when 'sonar.forceAuthentication' is set to 'true')
	sonar.login=admin
	sonar.password=admin

**7.** Create a new *SONAR_RUNNER_HOME* environment variable set to the install directory and add *$SONAR_RUNNER_HOME/bin* to the path by editing the *~/.bashrc* file

	export SONAR_RUNNER_HOME=/opt/sonar-runner-2.4/
	export PATH=$PATH:$SONAR_RUNNER_HOME/bin

**8.** Evaluate the content of the file with the following command

`source ~/.bashrc`

**9.** Check the basic installation executing the command *sonar-runner -h* and if the message is like as below, go to the next step

	usage: sonar-runner [options]

	Options:
	 -D,--define <arg>     Define property
	 -e,--errors           Produce execution error messages
	 -h,--help             Display help information
	 -v,--version          Display version information
	 -X,--debug            Produce execution debug output

**10.** Run the following command from the project base directory to launch the analysis

`sonar-runner`

**11.** Access [localhost:9000](http://localhost:9000) again to see the results of the analysis
