# docker image 만들기 

#### - python flask를 docker image로 실행시키기
#### - Linux 환경에서 실행




1. 디렉토리 생성 및 파일 생성 

        $ mkdir docker_image_making 
        $ cd docker_image_making 

    - requirements.txt 파일 생성 
 
            $ echo "Flask==0.12.2" > requirements.txt 
            $ touch hello.py 
            $ vi requirements.txt             

  - requirements.txt에 들어갈 내용 
  
          Flask==0.12.2 
          bs4 
          requests

- Dockerfile 생성

        $ vi Dockerfile
    - 아래 내용을 입력한 후, ESC 버튼을 누르고 :wq 를 입력하여 파일을 저장한다.
 
          FROM python
          COPY . /app
          WORKDIR /app
          RUN pip install flask
          EXPOSE 5000
          CMD ["python", "hello.py"]

 - python flask hello.py 파일 생성
            - 에러가 난다면 $ pip3 install flask 또는 $ pip install flask를 본인의 python 버전에 맞게 실행시켜 라이브러리를 다운받는다.
            - 그래도 에러가 난다면 $ pip uninstall beautifulsoap 또는 $ pip uninstall beautifulsoap4를 해보자!

                from flask import Flask
                app = Flask(__name__)

                @app.route("/")
                def hello():  
                        return "Hello World!"

                if __name__=='__main__':
                    app.run(debug=True,host='0.0.0.0')


2. 도커 이미지 만들기

 - 이제 파일들을 다 생성했다면 도커 이미지를 만들 차례이다. 

        $ docker build --tag [이미지명] 
        ex) $ docker build --tag image-test 

- 잘 만들어 졌는지 확인하기. 

        $ docker inage ls 

- 실행시키기 

        $ docker run -d -p 5000:5000 image-test 

- 현재 실행되고 있는 파일 확인하기 

        $ docker ps 




  
  
