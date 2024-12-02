---
title: Pygame으로 윷놀이 게임 만들기
author: soooyeon22
date: 2024-11-14 11:53:00 +0900
categories: [Projects]
tags: [pygame,Github]
---
![img10](https://soooyeon22.github.io/assets/img/favicons/img10.png)

## 🎯 프로젝트 소개

파이게임(Pygame)을 사용하여 전통 윷놀이 게임을 구현했습니다. 이 프로젝트는 **두 명 이상의 플레이어가 참여하는 윷놀이**를 기반으로 하며, 말 이동, 턴제 시스템 등을 포함합니다. 아래에서 구현 과정을 설명하고 주요 코드를 공유합니다.

---

📎전체코드 링크

[Github Repository](https://github.com/SKHU-OSS-2024-2/pygame-alpha-mine-sweeper)

## 게임설명

- 마우스를 사용해 버튼을 눌러 조작합니다.

<게임 설정> 

- PvP 형식입니다.
- Player는 2~4명입니다.
- 윷놀이의 말은 4개입니다.
- 말의 첫 시작 위치는 우측 하단입니다.
- 도착 지점을 초과해야 골인됩니다.
- 먼저 말이 4개 도착한 Player가 승리합니다.

<게임 룰>

- Player 1이 윷을 던집니다.
- Player 1이 나온 윷 만큼 이동합니다.
- Player 2가 윷을 던집니다.
- Player 2가 나온 윷 만큼 이동합니다.
- 윷 또는 모가 나올 경우 윷을 한 번 더 던집니다.
- 적군의 말을 잡을 경우 윷을 한 번 더 던집니다.
- 아군의 말과 마주친 경우 업힙니다.
- 윷판의 각 모서리, 혹은 정중앙에 도착할 경우 꺾어 움직일 수 있습니다.
- 윷판에 아군의 말이 존재할 경우 새로운 말을 꺼낼 건지, 본래 있던 말을 움직일 건지 선택할 수 있습니다.

<시작화면>

![img11](https://soooyeon22.github.io/assets/img/favicons/img11.png)

<게임 화면>

![img12](https://soooyeon22.github.io/assets/img/favicons/img12.png)

---

## 📂 프로젝트 구조

```
project/
├── main.py          # 게임 실행 및 초기화
├── Node.py          # 윷놀이판 노드 구조 정의
├── Player.py        # 플레이어 클래스 정의
├── Game.py          # 게임 진행을 관리
├── gameboard.py     # 화면에 게임판 및 말 표시
├── Horse.py         # 말 클래스 정의
```

---

## 🛠️ 주요 기능

### 1. **`Node.py`: 윷놀이판의 경로** ((Node))

윷놀이판의 각 위치를 `Node`로 정의하고, 연결합니다.

### **주요 코드**

```python
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None
        self.prev = None
```

- **`value`**: 각 노드의 고유 값(위치 번호).
- **`next`, `prev`**: 각 노드의 다음 및 이전 위치를 연결.

```python
class DoublyLinkedList:
    def create_structure(self):
        for i in range(6):
            self.add_node(i)
            if i > 0:
                self.connect_nodes(i - 1, i)
        # 교차 경로 설정
        self.connect_nodes(24, 15)
```

- **`create_structure`**: 게임판의 경로를 설정하며, 일반 경로와 특수 경로(교차점)를 포함합니다.

---

### 2. **`Player.py`: 플레이어 관리** ((Player))

플레이어와 주사위(윷 던지기) 기능을 제공합니다.

### **주요 코드**

```python
class Player:
    def __init__(self, player_id, num_horses, board):
        self.player_id = player_id
        self.horses = [Horse.Horse(i + 1, board) for i in range(num_horses)]
```

- **`player_id`**: 플레이어의 ID.
- **`horses`**: 플레이어가 보유한 말 리스트.

```python
def roll_dice(self):
    return random.choice([-1, 1, 2, 3, 4, 5])
```

- -1: "백도", 1~5: 도, 개, 걸, 윷, 모의 결과.

---

### 3. **`Horse.py`: 말 관리** ((Horse))

플레이어의 말을 정의하고, 말의 위치를 관리합니다.

### **주요 코드**

```python
class Horse:
    def __init__(self, horse_id, board):
        self.horse_id = horse_id
        self.position = board.nodes[0]
```

- **`horse_id`**: 말의 고유 ID.
- **`position`**: 현재 말의 위치(초기값: Node(0)).

```python
def __repr__(self):
    return f"Horse {self.horse_id} at Node {self.position.value}"
```

- 말의 ID와 현재 위치를 출력.

---

### 4. **`Game.py`: 게임 진행 관리** ((Game))

플레이어와 윷놀이판을 초기화하고, 각 플레이어의 턴을 관리합니다.

### **주요 코드**

```python
class Game:
    def __init__(self):
        self.board = Node.DoublyLinkedList()
        self.board.create_structure()
        self.players = [Player.Player(i + 1, 4, self.board) for i in range(2)]
```

- **`self.board`**: 게임판의 경로를 설정.
- **`self.players`**: 플레이어와 해당 말을 초기화.

```python
def play_round(self):
    for player in self.players:
        dice_result = player.roll_dice()
        print(f"Player {player.player_id} 주사위 결과: {dice_result}")
```

- 각 플레이어가 윷을 던지고 결과를 출력.

---

### 5. **`gameboard.py`: 게임판 시각화** ((gameboard))

Pygame을 통해 게임판과 말을 화면에 표시합니다.

### **게임판 그리기**

```python
def draw_board():
    screen.fill(WHITE)
    pygame.draw.rect(screen, BEIGE, (70, 70, 650, 750))
    for pos in board_positions:
        pygame.draw.circle(screen, BLACK, pos, 20)
```

### **윷 던지기 및 말 이동**

```python
class Piece:
    def move(self, steps):
        if steps == -1:
            self.position = max(0, self.position - 1)  # 백도 처리
        else:
            self.position = min(self.position + steps, len(board_positions) -1)
```

- **`steps`**: 윷 던지기의 결과에 따라 이동 거리 결정.

### **게임 루프**

```python
def gameboard():
    while True:
        for event in pygame.event.get():
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_SPACE:  
                    result, steps = throw_yut()
                    print(f"{turn} 팀의 윷 결과: {result}")
```

---

### 6. **`main.py`: 게임 실행** ((gameboard))

게임의 엔트리 포인트로, Pygame을 초기화하고 `gameboard`를 실행합니다.

### **주요 코드**

```python
if __name__ == "__main__":
    gameboard()
```

- `gameboard` 함수에서 Pygame 루프를 실행하며, 게임 진행을 관리합니다.

---