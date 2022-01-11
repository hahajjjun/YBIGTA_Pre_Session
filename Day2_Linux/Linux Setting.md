# Session 2. Linux

- Git bash → shell program
- wget
- Ubuntu Virtual Machine
    - `sudo apt-get update`
    - `sudo apt-get install python3-venv`
    - `mkdir ybSession`
    - `python3 -m venv myenv`
    - `source ~/myenv/bin/activate` : activate virtual environment
- Inside `myenv`
    - `nano hello.py`
        - `print("hello world")`
        - `python hello.py`
            - output : hello world
    - `vim message.txt`
        - Depndencies
            - `sudo apt-get install vim-gtk3`  : enables copy-paste with Window OS clipboard
                - 그래도 안됨..
            - 혹은 setting에서 양방향 클립보드 공유 허용
                - 그래도 안됨..
                - **`sudo apt-get install virtualbox-guest-additions-iso`**
                - **`sudo apt-get install virtualbox-guest-utils`**
                    
                    했는데 안됨...
                    
        - 해결책
            - 일단 게스트 CD 이미지를 추가로 삽입해야 하는데 오류가 생겨서 그런 것
            - 설정-디스플레이- 그래픽컨트롤러 - VboxVGA 로 변경한 뒤 실행
            - 게스트 CD 이미지 삽입하면 문제 해결