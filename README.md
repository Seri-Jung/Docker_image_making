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
              
   ![pythonfile](https://user-images.githubusercontent.com/69622147/110907520-df2fb480-8350-11eb-9680-406c38248bdc.png)
        
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
                    
    ![파이썬](https://user-images.githubusercontent.com/69622147/110907506-da6b0080-8350-11eb-9d3d-7e167e5d91d8.png)
            
- 파이썬 파일이 잘 실행되는지 확인하기

        $ python3 hello.py 
        
   ![pythonfile](https://user-images.githubusercontent.com/69622147/110906756-beb32a80-834f-11eb-8dd2-868dee860072.png)
                
                
2. 도커 이미지 만들기

 - 이제 파일들을 다 생성했다면 도커 이미지를 만들 차례이다. 

        $ docker build --tag [이미지명] 
        ex) $ docker build --tag image-test 
        
   ![imagemaking](https://user-images.githubusercontent.com/69622147/110906755-beb32a80-834f-11eb-82cd-3195e066f07b.png)

- 잘 만들어 졌는지 확인하기. 

        $ docker image ls 
        
   ![dockerfind](https://user-images.githubusercontent.com/69622147/110906751-bd81fd80-834f-11eb-88cb-bd70f05edbc6.png)

- 실행시키기 

        $ docker run -d -p 5000:5000 image-test 

- 현재 실행되고 있는 파일 확인하기 

        $ docker ps 
        
   ![실행](https://user-images.githubusercontent.com/69622147/110907511-dc34c400-8350-11eb-97aa-9799d95d18a4.png)

3. 포트포워딩 및 실행 된 화면 


   ![결과](https://user-images.githubusercontent.com/69622147/110906757-bf4bc100-834f-11eb-9d6e-71f36d183aa1.png)




  
  
