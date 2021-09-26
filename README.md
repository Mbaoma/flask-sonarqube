# SonarQube as code health checker for Flask project

## Build the Flask project

- Create and switch to a virtual environment

```bash
python3 -m venv venv
source venv/bin/activate
```

- Install requirements

```bash
pip3 install -r requirements.txt
```

- Run the project

```bash
python3 main.py
```

## Install SonarQube

- Install SonarQube using Docker

```bash
docker run -d --name sonarqube -e SONAR_ES_BOOTSTRAP_CHECKS_DISABLE=true -p 9000:9000 sonarqube:latest
```

- Run SonarQube locally

```bash
http://localhost:9000/
```

**Default username and password is ```admin``` for both fields.**
**If asked to update password, kindly do so**

![image](https://user-images.githubusercontent.com/49791498/134785465-7fca5199-a354-4a1f-ad76-7dcf45f2406a.png)

## Run an Analysis on SonarQube

- We run an analysis manually, by clicking on the 'manually' option at the bottom of the page
![image](https://user-images.githubusercontent.com/49791498/134785499-093a3bdb-6979-44fc-a09a-f0976eacdaf6.png)

- Fill the prompts and tell SonarQube to run your project locally
![image](https://user-images.githubusercontent.com/49791498/134785569-1cb38df9-3f35-49af-b806-51d9c7fb574c.png)

- Generate a token
![image](https://user-images.githubusercontent.com/49791498/134785589-7e37b7f9-a8e1-41de-be9b-b06908fc28c5.png)

- For our build, we select the 'Other' option, when asked what describes our build.
We also have to download a scanner based on our operating system.
![image](https://user-images.githubusercontent.com/49791498/134785653-941fe477-d121-4649-9191-747f61c54555.png)

- We install SonarQube scanner following the prompts in [this article](https://techexpert.tips/sonarqube/sonarqube-scanner-installation-ubuntu-linux/).

```bash
wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.2.0.1873-linux.zip
unzip sonar-scanner-cli-4.2.0.1873-linux.zip
sudo mv sonar-scanner-4.2.0.1873-linux /opt/sonar-scanner
```

- Edit the ```sonar-scanner.properties``` file

```bash
```

to contain

```bash
sonar.host.url=http://localhost:9000
sonar.sourceEncoding=UTF-8
```

- Create a file to automate the required environment variables configuration

```bash
sudo nano /etc/profile.d/sonar-scanner.sh
```

to contain

```bash
#/bin/bash
export PATH="$PATH:/opt/sonar-scanner/bin"
```

- Add the sonar-scanner commands, to PATH variables

```bash
source /etc/profile.d/sonar-scanner.sh
```

- Verify that the PATH variable was changed as expected

```bash
env | grep PATH
```

![image](https://user-images.githubusercontent.com/49791498/134826437-26d65cba-1994-4dcd-8a74-57d320d3cd1f.png)

- Verify SonarQube scanner was installed

```bash
sonar-scanner -v
```

![image](https://user-images.githubusercontent.com/49791498/134826460-57443393-637e-4a30-a5d4-0172affdde11.png)

- Next, run the command as marked in red ink in the picture below.

The command should be ran in the directory where you installed SonarQube

![image](https://user-images.githubusercontent.com/49791498/134826480-9e98dbc6-2f4b-4bdf-9a69-c08df137fe9b.png)

**Expected result**

![image](https://user-images.githubusercontent.com/49791498/134826527-6d7648cf-cbf2-4998-afe8-69262c81816e.png)

**SonarQube web page**

![image](https://user-images.githubusercontent.com/49791498/134826550-a2e5b306-e86e-428c-aeb6-6f0190570d44.png)
