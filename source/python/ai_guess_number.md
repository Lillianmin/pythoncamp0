# AI Guess the Number
##目的
- 唯一作业:
  + 猜数游戏AI版
- 期待:
  + 抽象你的自然思维
  + 在尽可能短的代码行数中完成:无人介入的猜数游戏
  + 最好能动画式演示游戏过程
- 要求:
  + 基础: 用程序模拟出自己猜数的策略, 并进行检验
  + 可用: 用自制的猜数AI, 和自己的游戏对战
  + 合格: 猜数AI的游戏过程,可记录,可回放
  + 天才: 猜数AI的游戏过程,可记录,可回放,可分享,加载...进一步的:
    * 通过大量的游戏对战,统计自个儿AI 的能力?! 
    * 发布他人的AI 也可以接入的服务?
    * 并行多组游戏?
    * 怎么证明自个儿的 AI 策略是最优的?能用最少次数猜中?
- 教程期待:
  + 向 6个月 前看过以往自己教程的自己认真描述
  + 怎么设计代码来减少行数完成这个任务?
  + 有哪些理解上的坑,如何能理解之?

## 教程习惯改进,提高教程与coding效率
+ 笔记:养成随时记录的习惯
  - 作业出来,将作业作为目的写进笔记
  - 写代码之前,先第一个目标进行分解,规划类,功能
  - 依据目的,不断迭代,每次迭代之前,先构思
  - 随时记录调试过程中的问题与解决方式
  - 随时记录每一个阶段的时间花费

##时间记录
+ 视频: 1.2h
+ 构思:
  - 第一阶段: 0.5h
+ 代码
  - 第一阶段:2h
+ 笔记:养成随时记录的习惯
  - 作业出来,将作业作为目的写进笔记
  - 写代码之前,先第一个目标进行分解,规划类
  - 依据目的,不断迭代,每次迭代之前,先构思
  - 随时记录调试过程中的问题与解决方式
  - 随时记录每一个阶段的时间花费
  - 0.5h

##构思过程
###实现单个AI自动猜数
* 出题者，负责初始猜数的范围、根据AI猜的数据计算新的猜数范围
* AI玩家，负责根据猜数范围，猜数据
* 考虑到之后会有同时多个游戏进行的需求，将一个游戏进行的过程封装至一个游戏类中，每一场游戏都是一个游戏对象
  游戏对象负责的游戏过程:出题者出题,AI猜数,出题者判断AI是否正确,不正确,给出新的范围,正确,结束.
####第一阶段具体的类设计
+ QuizSetter：
  - quiz()
  - judge(ai_guess, ai_name)
+ AIPlayer:
  - guess(min_value, max_value)
+ GuessNumberGame:
  - start()
####第一阶段改进
- 将输出画到canvas而不是在终端输出
###实现游戏的保存与回放
####
* 历史记录，负责一局游戏中，电脑出题记录，AI猜数记录，保存至文件，回放。
+ GameHistory:
  - add_quiz()
  - add_guess()
  - save()
  - play()


##调试中的问题
+ game.draw_text(canvas, [50, 50], 24, "Red")
  NameError: global name 'game' is not defined
  - 变量声明的代码必须要在函数里面调用该变量之前
  - 同理,函数也是一样的,必须要在调用该函数的代码块之前
+ game = GuessNumberGame()
  TypeError: __init__() takes no arguments (1 given)
  game.draw_text(canvas, [50, 50], 24, "Red")
  TypeError: draw_text() takes exactly 4 arguments (5 given)
  - 在类的函数中,第一个参数总是self
  - 函数在调用之时,从代码看只传递了4个参数,实际上有将调用该函数的对象作为第一个参数传递进去
+ def print():
           ^
  SyntaxError: invalid syntax
  - 是因为函数名称比较特别吗?
+ canvas.draw_text(self.quiz.message, pos, size, color)
  AttributeError: QuizSetter instance has no attribute 'message'
  - self.message要在__init__中初始化过才有效
+ return True
   ^
  IndentationError: unexpected indent
  - 缩进不对
+ quiz_range = quiz.quiz()
  NameError: global name 'quiz' is not defined
  - 在__init__中以self.quiz初始化的对象,在调用时,必须以self.quiz调用
  - 也可以在__init__之外,初始化quiz对象,这样就可以直接用quiz调用了
+ guess = self.ai.guess(quiz_range[0], quiz_range[1])
  TypeError: 'int' object is not callable
  - 类中有一个变量叫guess,函数名与变量名一致时会导致这样的错误
  - 避免函数名与变量名名字一致
+ global game, game.quiz.message
                     ^
  SyntaxError: invalid syntax
  global game, game.self.quiz.message
                      ^
  SyntaxError: invalid syntax
  - 在init中以self.quiz形式初始化的对象,无法在类外部以game.quiz形式访问
  - self只能在类内部访问
+ game.start()在frame.start()之后调用,print到终端的输出要在关闭了frame后才会输出
  - 难道是frame.start()阻塞了进程了?
  - 将game.start()放到frame.start()之前
