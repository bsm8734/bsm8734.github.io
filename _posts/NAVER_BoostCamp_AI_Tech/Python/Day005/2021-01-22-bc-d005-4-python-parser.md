---
title: "[부스트캠프 AI Tech / Day5] 파이썬 arg/config-parser"
date: 2020-01-22 20:34:00 +0900
categories: [네이버 부스트캠프 AI Tech, Python] # Python
tags: [Python] # CS, 운영체제, Python
---


## **[DAY 5] Parser**

---

### **상태를 저장하거나 상태를 입력하는 방법**

1. configparser - 파일에 저장
2. argparser - 실행시점에 가져옴

### **configparser**

- 프로그램의 실행 설정을 file에 저장함
- Section, Key, Value 값의 형태로 설정된 설정 파일을 사용
- 설정파일을 Dict Type으로 (관리) 호출후 사용

- **config file**

    ```python
    """
    [SectionOne] // section- 대괄호
    Status: Single
    Name: Derek
    Value: Yes
    Age: 30
    Single: True
    // 속성 - key:value

    [SectionTwo]
    FavoriteColor = Green

    [SectionThree]
    FamilyName: Johnson
    """
    ```

- **configparser file**

    ```python
    import configparser
    config = configparser.ConfigParser()
    config.sections()

    config.read('example.cfg')
    config.sections()

    for key in config['SectionOne']:
    print(key)
    config['SectionOne']["status"]

    """
    'example.cfg'
    [SectionOne]
    Status: Single
    Name: Derek
    Value: Yes
    Age: 30
    Single: True
    [SectionTwo]
    FavoriteColor = Green
    [SectionThree]
    FamilyName: Johnson
    """
    ```

### **argparser**

- 콘솔창에서 실행할 때, 세팅 정보를 전달
- Console 창에서 프로그램 실행시 Setting 정보를 저장함
- 거의 모든 Console 기반 Python 프로그램 기본으로 제공
- 특수 모듈도 많이 존재하지만(TF), 일반적으로 argparse를 사용
- Command-Line Option 이라고 부름
- 커맨드라인 옵션이라고도 함
- arg 가이드라인을 제공할 수 있음
- usage처럼 사용할 수 있음-?
- 타입과 같은 것을 검증 가능
- arg 미리 넣어둬서 사용자가 실험해볼 수 있도록 만들어둠

    ```python
    import argparse
    parser = argparse.ArgumentParser(description='Sum two integers.')

    # 짧은 이름, 긴 이름, 표시 명, help 설명, argument type
    parser.add_argument('-a', "--a_value", dest=”A_value", help="A integers", type=int)
    parser.add_argument('-b', "--b_value", dest=”B_value", help="B integers", type=int)
    args = parser.parse_args()
    print(args)
    print(args.a)
    print(args.b)
    print(args.a + args.b)
    ```

    ```python
    def main():
        parser = argparse.ArgumentParser(description='PyTorch MNIST Example')
        parser.add_argument('--batch-size', type=int, default=64, metavar='N', help='input batch size for training (default:
        64)')
        parser.add_argument('--test-batch-size', type=int, default=1000, metavar='N', help='input batch size for testing
        (default: 1000)')
        parser.add_argument('--epochs', type=int, default=10, metavar='N', help='number of epochs to train (default: 10)')
        parser.add_argument('--lr', type=float, default=0.01, metavar='LR', help='learning rate (default: 0.01)')
        parser.add_argument('--momentum', type=float, default=0.5, metavar='M', help='SGD momentum (default: 0.5)')
        parser.add_argument('--no-cuda', action='store_true', default=False, help='disables CUDA training')
        parser.add_argument('--seed', type=int, default=1, metavar='S', help='random seed (default: 1)’)
        parser.add_argument('--save-model', action='store_true', default=False, help='For Saving the current Model')
        args = parser.parse_args()

    if __name__ == '__main__':
        main()
    ```
