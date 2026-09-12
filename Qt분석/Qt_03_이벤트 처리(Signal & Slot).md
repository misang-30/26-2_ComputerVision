## 1.이벤트 처리 (Signal & Slot)

사용자의 동작(클릭, 입력 등)이 일어났을 때 특정 함수가 실행되도록 연결하는 Qt의 핵심 메커니즘입니다.

- **Signal (시그널)**: 이벤트가 발생했음을 알리는 신호 (예: 버튼 클릭 `clicked`)
    
- **Slot (슬롯)**: Signal을 받아 실제 로직을 수행하는 함수
### 1). 헤더 파일 (`mainframe.h`)


``` c++
#ifndef MAINFRAME_H
#define MAINFRAME_H

#include <QWidget>
#include <QLabel>
#include <QPushButton>

class MainFrame : public QWidget {
    Q_OBJECT // Signal & Slot 사용을 위한 필수 마크로

public:
    MainFrame(QWidget *parent = nullptr);

signals:
    // 사용자 정의 시그널 (구현부 필요 없음)
    void customSignal(const QString &message);

private slots:
    // 시그널을 받아 처리할 슬롯 함수
    void onButtonClicked();
    void handleCustomSignal(const QString &message);

private:
    QLabel *label;
    QPushButton *btn;
};

#endif
```

### 2). 소스 파일(`mainframe.cpp`)

``` c++
#include "mainframe.h"
#include <QVBoxLayout>

MainFrame::MainFrame(QWidget *parent) : QWidget(parent) {
    label = new QLabel("버튼을 눌러보세요.", this);
    btn = new QPushButton("클릭", this);

    QVBoxLayout *layout = new QVBoxLayout(this);
    layout->addWidget(label);
    layout->addWidget(btn);

    // [Signal & Slot 연결]
    // 1. 버튼 클릭 -> onButtonClicked 슬롯 호출
    connect(btn, &QPushButton::clicked, this, &MainFrame::onButtonClicked);

    // 2. 사용자 정의 시그널 -> handleCustomSignal 슬롯 호출
    connect(this, &MainFrame::customSignal, this, &MainFrame::handleCustomSignal);
}

void MainFrame::onButtonClicked() {
    // 버튼 클릭 시 커스텀 시그널 발생(emit)
    emit customSignal("시그널이 성공적으로 전달되었습니다!");
}

void MainFrame::handleCustomSignal(const QString &message) {
    // 전달받은 메시지로 라벨 텍스트 변경
    label->setText(message);
}
```