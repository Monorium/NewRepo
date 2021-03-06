```plantuml
@startuml
title ユースケース図 - Communication Board
skinparam ComponentStyle uml2
left to right direction

actor "Controller" as Controller
actor "Main Board" as MainBoard_act

rectangle "WebSocket Server" as WebSocketServer {
  usecase "WebSocketを接続する" as ucConnectSocket
  usecase "WebSocketを切断する" as ucDisconnectSocket
  rectangle "電文を送信する" {
    usecase "ヘルスチェックを送信する" as ucSendHealthCheck
    usecase "サーボの角度を変更する" as ucChangeServoAngle
    usecase "16方向移動を命令する" as ucCmdDirectionMove
    usecase "回転方向移動を命令する" as ucCmdRollingMove
    usecase "動作を停止する" as ucPause
    usecase "基本姿勢に変更する" as ucChangeBasicPosition
  }
}
rectangle "Servo Control" as ServoControl {
  usecase "サーボの角度を変更する" as ucChangeServoAngle_local
}

actor "Main Board" as MainBoard
actor "Servo_11~18" as Servo_11

Controller -- ucConnectSocket
Controller -- ucSendHealthCheck
Controller -- ucDisconnectSocket
Controller -- ucChangeServoAngle
Controller -- ucCmdDirectionMove
Controller -- ucCmdRollingMove
Controller -- ucPause
Controller -- ucChangeBasicPosition
MainBoard_act -- ucChangeServoAngle_local

ucChangeServoAngle -- MainBoard
ucCmdDirectionMove -- MainBoard
ucCmdRollingMove -- MainBoard
ucPause -- MainBoard
ucChangeBasicPosition -- MainBoard
ucChangeServoAngle_local -- Servo_11

@enduml
```
