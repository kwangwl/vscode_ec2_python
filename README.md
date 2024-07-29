# VsCode on EC2 with Amazon Linux 2023 & Python 3.9

이 CloudFormation 템플릿은 Amazon Linux 2023과 Python 3.9이 설치된 EC2 인스턴스를 설정합니다.
이 인스턴스는 사전에 VS Code 서버와 지정된 Git 저장소를 클론하도록 구성되어 있습니다.

## 파라미터

- `Region`: 리소스가 배포될 AWS 리전. 기본값은 `us-west-2`.
- `InstanceType`: EC2 인스턴스 유형. 기본값은 `t3.xlarge`.
- `AMIType`: EC2 인스턴스를 위한 Amazon Linux 버전. 기본값은 `AmazonLinux2023`.
- `AmazonLinux2023AmiId`: Amazon Linux 2023 AMI ID.
- `GitRepositoryUrl`: 클론할 Git 저장소의 URL.

## 리소스

### VPC

지정된 CIDR 블록을 가진 VPC를 생성합니다.

### 인터넷 게이트웨이

인터넷 게이트웨이를 생성하고 VPC에 연결합니다.

### 서브넷

VPC 내에 퍼블릭 서브넷을 생성합니다.

### 라우트 테이블

라우트 테이블을 생성하고 퍼블릭 서브넷에 연결하여 인터넷 액세스를 가능하게 합니다.

### 보안 그룹

SSH, HTTP, HTTPS 액세스를 허용하는 보안 그룹을 생성합니다.

### IAM 역할

EC2 인스턴스를 위한 IAM 역할 및 인스턴스 프로파일을 생성합니다.

### EC2 인스턴스

Amazon Linux 2023을 사용하여 EC2 인스턴스를 생성하고, Python 3.9, VS Code 서버를 설치하며, 지정된 Git 저장소를 클론합니다.
또한 git repository 의 requirements.txt 에 있는 패키지를 설치하고, vscode 코드 실행시 해당 repsitory 기준으로 실행됩니다.

## 출력

- `EC2InstancePublicIP`: VS Code 서버 EC2 인스턴스의 공용 IP 주소.
