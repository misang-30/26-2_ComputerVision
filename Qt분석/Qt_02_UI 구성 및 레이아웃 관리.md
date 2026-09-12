## 1. UI 구성 및 레이아웃 관리 (Layout & Widgets)


- **위젯 (Widget):** 상자 안에 들어가는 **'물건'** (예: 버튼, 입력창, 이미지)
    
- **레이아웃 (Layout):** 물건을 정돈해 넣는 **'수납장/틀'** (예: 가로 정렬, 세로 정렬)
### 1). 레이아웃
- C++에서는 `QLayout` 포인터 객체를 생성하여 위젯을 추가(`addWidget`)한 뒤, 부모 위젯에 `setLayout()`으로 적용합니다.

- **`QVBoxLayout`**: 위젯을 수직(위$\rightarrow$아래)으로 정렬
- **`QHBoxLayout`**: 위젯을 수평(왼쪽$\rightarrow$오른쪽)으로 정렬
- **`QGridLayout`**: 위젯을 **격자(행, 열)** 형태로 정렬

### 2). **자주 쓰는 기본 위젯 (Widgets)**
- Qt에서 위젯은 화면에서 보이는 모든 UI 구성 요소를 의미합니다.
- 버튼, 텍스트 상자, 이미지 출력 창, 체크박스 등 사용자가 눈으로 보고 클릭하거나 값을 입력하는 모든 객체가 전부 위젯입니다.

- `QLabel`: 텍스트나 이미지를 출력하는 창.
- `QPushButton`: 클릭 가능한 버튼.
- `QLineEdit`: 한 줄 텍스트 입력창.

**C++ 예제 코드 (`MainFrame.cpp`)**
``` c++
#include "mainframe.h"
#include <QVBoxLayout>
#include <QHBoxLayout>
#include <QLabel>
#include <QLineEdit>
#include <QPushButton>

MainFrame::MainFrame(QWidget *parent) : QWidget(parent) {
    // 1. 위젯 동적 생성
    QLabel *label = new QLabel("이름 입력:", this);
    QLineEdit *inputField = new QLineEdit(this);
    QPushButton *btn = new QPushButton("확인", this);

    // 2. 레이아웃 생성 및 위젯 배치
    QHBoxLayout *hLayout = new QHBoxLayout(); // 수평
    hLayout->addWidget(label);
    hLayout->addWidget(inputField);

    QVBoxLayout *mainLayout = new QVBoxLayout(); // 수직
    mainLayout->addLayout(hLayout);              // 레이아웃 중첩 가능
    mainLayout->addWidget(btn);

    // 3. 메인 윈도우에 레이아웃 적용
    this->setLayout(mainLayout);
    this->setWindowTitle("C++ Qt Layout 예제");
    this->resize(300, 150);
}
```

