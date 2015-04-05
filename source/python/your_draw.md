# Your Draw

## 目标
- 可回放的点彩画板
- 期待:
    + 三种形状画笔可选: 三角/方形/圆形
    + 颜色可定义: 颜色名 或是 RGB 声明
    + 每次 鼠标 点击画板任意一处,都绘制一个当前画笔可用彩色形状
    + 可记录1024次点彩绘制行为
    + 可回放整个记录的绘制行为
- 要求:
    + 基础: 有画笔,可点绘
    + 可用: 有画笔,有颜色,可点绘
    + 合格: 有画笔,有颜色,可点绘,可回放
    + 天才: 有画笔,有颜色,可点绘,可回放,回放速度可调节,回放可输出为文件
    
## 学习时间统计
* 视频学习。2h，公交上完成。重点截屏。
* simplegui本地环境(环境搭建时，写笔记)。1h(Ubuntu)+5.5h(Windows,坑）。
* 基本功能coding。8h。
* 附加功能。3h(文件知识点学习+测试程序)+2h(整合进Draw)
* 教程。0.5h(python基础)+1h(基本功能的流程图)+3h(本文)

## 开发流程
* 以本地代码仓库为主，当要提交V1/V2作业时，再将代码在codeskulptor中打开，调试后提交。V3完全在本地开发。
在codeskulptor中调试时发现与本地冲突如下：

  * 本地Tab，占8个空格。codeskulptor占四个。对策：严格按照四个空格来缩进。
  * global 在函数中声明时，本地可以在子快中，比如else后，而codeskulptor不行。对策：不在函数子块中声明global。

* 寻找知识源头
  * 在google与stackoverflow寻找提示
  * 在python.org查找需要用到的知识点
  * 善用pydoc（windows: python -m pydoc 查看帮助

## 构思
### 基本功能
* 实现基本的点彩绘图、选择形状
* 添加颜色设置，绘图时，之前的图案不丢失
* 添加timer，添加回放，完成V1
* 添加Color Picker，完成V2

### 附加功能
* 添加文件的保存，与打开文件回放。完成V3。


## 基本功能实现
* ![基本功能流程图](image/Your_Draw.png)

### 实现基本的点彩绘图、选择形状
  * frame 添加Circle, Square, Triangle形状选择按钮,完成形状设置
  ```
def shape_circle():
def shape_triangle():
def shape_square():
frame.add_button("Circle", shape_circle)
frame.add_button("Triangle", shape_triangle)
frame.add_button("Square", shape_square)
  ```

  * 通过鼠标位置，计算正方形、三角形的所有点坐标
  ```
def get_square_points(x, y, length):
def get_triangle_points(x, y, length):
  ```
  * frame添加鼠标点击事件处理，在画布上画出当前形状
  ```
def draw(canvas):
        canvas.draw_circle(pos, 30, 2, "Black", "Red")
        canvas.draw_polygon(get_triangle_points(pos, 60), 2, "Black", "Red")
        canvas.draw_polygon(get_square_points(pos, 60), 2, "Black", "Red")
def mouse_click(pos):
frame.set_mouseclick_handler(mouse_click)
  ```

### 添加颜色设置，绘图时，之前的图案不丢失
* 颜色设置，颜色名称与颜色RGB输入合法性检测
  * color_list存放所有color name
  * 颜色设置时，合法性检测
  ```
  def color_rgb_reg(color):
      return re.match(r'#[0-9a-f]{6}', color, re.IGNORECASE)
  if (color in color_list) or color_rgb_reg(color):
      cur_color = color
  ```
* 使用dictionary存放单个点的信息
```
{"x":x, "y":y, "shape":shape, "color":color}
```
* 使用list存放所有点的信息，当鼠标点击时，在mouse_click处理函数中，向list.append(dictionary)
```
shape={"x":pos[0], "y":pos[1], "shape":cur_shape, "color":cur_color}
 shape_list.append(shape)
```
* 绘制所有shape
```
def draw(canvas):
    for shape in shape_list:
        draw_shape(canvas,shape)

def draw_shape(canvas, shape):
    if shape["shape"] == "Circle":
        canvas.draw_circle([shape["x"], shape["y"]], 30, 2, "Black", shape["color"])
    elif shape["shape"] == "Triangle":
        canvas.draw_polygon(get_triangle_points(shape["x"], shape["y"], 60), 2, "Black", shape["color"])
    elif shape["shape"] == "Square":
        canvas.draw_polygon(get_square_points(shape["x"], shape["y"], 60), 2, "Black", shape["color"])
    else:
        canvas.draw_point([shape["x"], shape["y"]], shape["color"])
```
### 添加timer，添加回放，完成V1
* 设置定时器interval需要在timer stop后，设置才有效
```
def set_interval(input_interval):
    if play_mode:
        show_message("Please don't Change Interval When Playing!")
        return
    global interval,message,timer
    try:
        interval = int(input_interval)
        timer = simplegui.create_timer(interval, timer_handler)
    except ValueError:
        show_message("Please Input a Integer for Interval!")
        interval_input.set_text("")
```
* play/stop按钮，作为toggle按钮，可以进行开始和停止控制
```
def play_stop():
    global message,play_mode,play_index
    if play_stop_btn.get_text() == "Play":
        play_mode=True
        play_stop_btn.set_text("Stop")
        play_index = 0
        timer.start()
    elif play_stop_btn.get_text() == "Stop":
        show_message("Play Stoped by User")
        play_end()
        play_index = -1
```

* 定时器ticker时，播放下一步。若已经播放完所有，则停止计时器。
```
def timer_handler():
    global play_index
    if (play_index >= 0 and play_index < (len(shape_list) - 1)):
        play_index += 1
    else:
        show_message("Play End")
        play_end()
```
### 添加Color Picker，完成V2
* 在canvas上画color picker,通过index获取到每个色块在画布上的坐标，index对应color_list中相应的颜色名称

```
def get_picker_points(index):
    column = index // COLOR_PICKER_ROW
    row = index % COLOR_PICKER_ROW
    pos = [COLOR_PICKER_WIDTH * column, COLOR_PICKER_WIDTH * row]
    return get_square_points(pos[0], pos[1], COLOR_PICKER_WIDTH)
```

* 点击color picker相应色块，设置当前颜色。通过鼠标点击的pos，判断是在color picker中的index，如果在color picker中，则返回相应的颜色index，否则，返回的index color picker index范围之内。在color picker中，则设置当前颜色，否则，绘制图形

```
def get_color_picker_index(pos):
    column = pos[0] // COLOR_PICKER_WIDTH
    row = pos[1] // COLOR_PICKER_WIDTH
    index = column * COLOR_PICKER_ROW + row
    return index
def mouse_click(pos):
    global cur_color
    color_picker_index = get_color_picker_index(pos)
    if color_picker_index < 0 or color_picker_index >= COLOR_PICKER_ROW * COLOR_PICKER_COLUMN :
        shape={"x":pos[0], "y":pos[1], "shape":cur_shape, "color":cur_color}
        shape_list.append(shape)
        global cur_index,message,mouse_mode
        cur_index=len(shape_list) - 1
        messaage=""
        mouse_mode="click"
    else:
        cur_color = color_list[color_picker_index]
```
## 附加功能实现
### 添加文件的保存，与打开文件回放。完成V3。
* 确定使用tkFileDialog，file来实现此功能
 - python.org搜索file\file selector
 - google python file selector

* 先写一个测试程序，完成对文件的保存、关闭、写、读操作的学习
  - pydoc tkFileDialog, 查看，初步确定使用下面两个函数来完成文件的保存于打开
  ```
tkFileDialog.asksaveasfile(mode='w')
tkFileDialog.askopenfile(mode='r')
  ```
  - 上面两个函数返回对象对象均为file，pydoc file,初步确定如下两个函数完成文件的读写
  ```
file.write(str)
file.readline(1024)
  ```
  - 编写测试程序,主要功能函数是：保存文件并写入内容；打开文件并读取内容。
  ```
def save_draw():
    save_file = tkFileDialog.asksaveasfile(mode='w')
    for index in range(5):
        save_file.write(str(index)+"\n")
    save_file.flush()
    save_file.close()
```
```
def open_draw():
    global shape_list
    end = False
    open_file = tkFileDialog.askopenfile(mode='r')
    while not end:
        shape_str = open_file.readline(1024)
        print(shape_str)
        if shape_str == "":
            end = True
        else:
            shape_list.append(shape_str)
    open_file.close()
  ```
  - [文件测试程序代码](https://github.com/Lillianmin/omooc.py/blob/master/src/iippy-2/test_file.py)
    - 问题
      - tk的dialog没有关闭。google之，[参考](http://bytes.com/topic/python/answers/768419-askopenfilename-tkfiledialog-problem)
      
    ```
    from Tkinter import *
    root = Tk()
    root.withdraw()
    ```
      
* 添加回放保存、与回放文件播放至最终代码中。
  * 这里比测试程序多的一个知识点是str转list，google之，[参考](http://stackoverflow.com/questions/1894269/convert-string-representation-of-list-to-list-in-python)
  * 最终保存文件、打开文件播放代码块如下
  ```
def save_draw():
    save_file = tkFileDialog.asksaveasfile(mode='w')
    save_file.write(str(shape_list))
    save_file.flush()
    save_file.close()
def open_draw():
    end = False
    shape_str = ""
    open_file = tkFileDialog.askopenfile(mode='r')
    while not end:
        read_str = open_file.readline(1024)
        print(shape_str)
        if not read_str:
            end = True
        else:
            shape_str += read_str
    open_file.close()
    print shape_str
    shape_list = ast.literal_eval(shape_str)
    play_stop()
  ```


## 成果
[code on pythoncamp0](https://github.com/Lillianmin/omooc.py/blob/master/src/iippy-2/your_draw.py)
### V1
[codeskulptor](http://www.codeskulptor.org/#user39_WzrwqDz913YgHET.py)

* draw
* color set
* timer
* play

Bug:
* set interval not work when playing

### V2
[codeskulptro](http://www.codeskulptor.org/#user39_qVvqibXQ0S8nydd.py)

* color picker

### V3
[code on pythoncamp0](https://github.com/Lillianmin/omooc.py/blob/master/src/iippy-2/your_draw.py)

* file save and play
* 本地需要安装simpleguics2game(依赖pygame,matplotlib）
