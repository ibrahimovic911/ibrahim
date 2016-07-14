# ibrahim
"Hello  جماعة الخير"
 # calc.py - a Python calculator 
2 from tkinter import * 
3 
 
4 # the main class 
5 class Calc(): 
6     def __init__(self): 
7         self.total = 0 
8         self.current = "" 
9         self.new_num = True 
10         self.op_pending = False 
11         self.op = "" 
12         self.eq = False 
13 
 
14     def num_press(self, num): 
15         self.eq = False 
16         temp = text_box.get() 
17         temp2 = str(num)       
18         if self.new_num == True: 
19             self.current = temp2 
20             self.new_num = False 
21         else: 
22             if temp2 == '.' and '.' in temp: 
23                     return 
24             self.current = temp + temp2 
25             while len(self.current) > 1 and self.current[0] == '0' and self.current[1] != '.': 
26                 self.current = self.current[1:] 
27         self.display(self.current) 
28 
 
29     def calc_total(self): 
30         self.eq = True 
31         self.current = float(self.current) 
32         if self.op_pending == True: 
33             self.do_sum() 
34         else: 
35             self.total = float(text_box.get()) 
36 
 
37     def display(self, value): 
38         text_box.delete(0, END) 
39         text_box.insert(0, value) 
40 
 
41     def do_sum(self): 
42         if self.op == "add": 
43             self.total += self.current 
44         elif self.op == "minus": 
45             self.total -= self.current 
46         elif self.op == "times": 
47             self.total *= self.current 
48         elif self.op == "divide" and self.current: 
49             self.total /= self.current 
50         else: 
51             self.total = 0 
52         self.new_num = True 
53         self.op_pending = False 
54         self.display(self.total) 
55 
 
56     def operation(self, op):  
57         self.current = float(self.current) 
58         if self.op_pending == True: 
59             self.do_sum() 
60         elif self.eq == False: 
61             self.total = self.current 
62         self.new_num = True 
63         self.op_pending = True 
64         self.op = op 
65         self.eq = False 
66 
 
67     def cancel(self): 
68         self.eq = False 
69         if self.new_num == False: 
70             self.current = "0" 
71             self.display(0) 
72             self.new_num = True 
73 
 
74     def all_cancel(self): 
75         self.cancel() 
76         self.new_num = False 
77         self.total = 0 
78 
 
79     def sign(self): 
80         self.eq = False 
81         self.current = -(float(text_box.get())) 
82         self.display(self.current) 
83 
 
84 
 
85 class My_Btn(Button): 
86     def btn_cmd(self, num): 
87         self["command"] = lambda: sum1.num_press(num) 
88 
 
89 
 
90 sum1 = Calc() 
91 root = Tk() 
92 calc = Frame(root) 
93 calc.grid() 
94 
 
95 root.title("Calculator") 
96 text_box = Entry(calc, justify=RIGHT) 
97 text_box.grid(row = 0, column = 0, columnspan = 3, pady = 5) 
98 text_box.insert(0, "0") 
99 
 
100 # make the buttons 
101 numbers = "789456123" 
102 i = 0 
103 bttn = [] 
104 for j in range(1,4): 
105     for k in range(3): 
106         bttn.append(My_Btn(calc, text = numbers[i])) 
107         bttn[i].grid(row = j, column = k, pady = 5) 
108         bttn[i].btn_cmd(numbers[i]) 
109         i += 1 
110 bttn_0 = Button(calc, text = "0") 
111 bttn_0["command"] = lambda: sum1.num_press(0) 
112 bttn_0.grid(row = 4, column = 1, pady = 5) 
113 
 
114 bttn_div = Button(calc, text = chr(247)) 
115 bttn_div["command"] = lambda: sum1.operation("divide") 
116 bttn_div.grid(row = 1, column = 3, pady = 5) 
117 
 
118 bttn_mult = Button(calc, text = "x") 
119 bttn_mult["command"] = lambda: sum1.operation("times") 
120 bttn_mult.grid(row = 2, column = 3, pady = 5) 
121 
 
122 minus = Button(calc, text = "-") 
123 minus["command"] = lambda: sum1.operation("minus") 
124 minus.grid(row = 3, column = 3, pady = 5) 
125 
 
126 point = Button(calc, text = ".") 
127 point["command"] = lambda: sum1.num_press(".") 
128 point.grid(row = 4, column = 0, pady = 5) 
129 
 
130 add = Button(calc, text = "+") 
131 add["command"] = lambda: sum1.operation("add") 
132 add.grid(row = 4, column = 3, pady = 5) 
133 
 
134 neg= Button(calc, text = "+/-") 
135 neg["command"] = sum1.sign 
136 neg.grid(row = 5, column = 0, pady = 5) 
137 
 
138 clear = Button(calc, text = "C") 
139 clear["command"] = sum1.cancel 
140 clear.grid(row = 5, column = 1, pady = 5) 
141 
 
142 all_clear = Button(calc, text = "AC") 
143 all_clear["command"] = sum1.all_cancel 
144 all_clear.grid(row = 5, column = 2, pady = 5) 
145 
 
146 equals = Button(calc, text = "=") 
147 equals["command"] = sum1.calc_total 
148 equals.grid(row = 5, column = 3, pady = 5) 
149 
 
150 root.mainloop() 
