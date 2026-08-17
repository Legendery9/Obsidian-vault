# 1. Definition
- Sample Space: không gian mẫu
- Set: Tập hợp
- Total propability
- X: biến ngẫu nhiên rời rạc
# 2. Cơ bản:
- Giao giữa 2 tập hợp - intersection $A \cap B$
- Điều kiên của A và B - conditional probability$A | B$
	- Biết chắc kết quả nằm trong B, hỏi xác suất nó thuộc A bao nhiêu -> chỉ nhìn các phần tử trong B
	- VD:$$
	  \begin{multline} 
	  Cho\space S={1,2,3,4,5,6} \\ 
	  A(các\space số \space chẵn )={2,4,6} \\ 
	  B(Các \space số \space >3) = {4,5,6} \\
	  P(A|B) =\frac{2}{3}
	  \end{multline}$$
	- Đảo chiều:  $P(B|A)=\frac{P(A\cap B)}{P(A)}$
- Equally likely - Đồng khả năng: $P(B|A)=\frac{n(A\cap B)}{n(A)}=\frac{\frac{n(A\cap B)}{n(S)}}{\frac{n(A)}{n(S)}}$
	- n(S) là số phần tử trong sample space
- Hợp của 2 tập hợp - union $A \cup B$
- Sample space: không gian mẫu - tập hợp tất cả sự kiện có thể xảy ra $$S = {1,2,3,4,5,6,7}$$
- Event: biến cố - 1 tập con của sample space
	- Ra số chẵn:$A={2,4,6}$
# 3. Các dạng propbability:
	1. A prior classical propbability - dựa trên lý thuyết, lý luận thuần tuý.
	2. Empirical propbability - dựa trên quan sát thực tế.
# 4. Data Type
	1. Discrete: đếm được
	2. Continuous: giao động
# 5. Xung khắc: 2 hoặc nhiều event không thể xảy ra đồng thời:
- Tức: $A\cap B = \emptyset$
- Hay: $P(A\cap B)=0$
# 6. Biến cố bao trùm
>1 Tập hợp có ít nhất 1 event trong đó chắc chắn xảy ra:

1. Nếu: $B_1​,B_2​,…,B_n$ bao trùm thì: $B1​\cup B2​\cup​ … ​\cup Bn = \Omega$
2. Với $\Omega$ là không gian mẫu
# 7. Biến cố đầy đủ:
- Điều kiện:
	- Là Biến cố bao trùm
	- Là đôi một xung khắc
	- Có xác suất dương:
		- $P(B_i)>0$