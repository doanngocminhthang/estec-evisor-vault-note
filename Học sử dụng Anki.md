Tuyệt vời! Anki là một công cụ cực kỳ hiệu quả để học thuộc lòng các flashcard này bằng phương pháp Lặp lại ngắt quãng (Spaced Repetition).

Để import vào Anki, cách tốt nhất là chuẩn bị một file văn bản đơn giản (như .txt hoặc .csv) theo một định dạng mà Anki có thể hiểu được.

Dưới đây là hướng dẫn chi tiết từng bước.

---

### **Bước 1: Chuẩn bị file dữ liệu**

1. **Mở một trình soạn thảo văn bản** đơn giản như Notepad (trên Windows), TextEdit (trên macOS), hoặc VSCode.
    
2. **Sao chép (Copy)** toàn bộ nội dung dưới đây. Tôi đã định dạng sẵn 40 flashcard theo cấu trúc Mặt trước<Ký tự phân cách>Mặt sau. Ký tự phân cách phổ biến nhất là dấu tab, nhưng ở đây tôi sẽ dùng dấu chấm phẩy ; để bạn dễ nhìn và chỉnh sửa hơn.
    
3. **Dán (Paste)** nội dung này vào file văn bản bạn vừa mở.
    

**Nội dung để copy:**

Generated code

```
Độ phức tạp thời gian (Time Complexity) là gì?;Là thước đo thời gian chạy của một thuật toán dưới dạng một hàm của kích thước đầu vào (n). Thường được biểu thị bằng ký hiệu Big O (ví dụ: O(n), O(log n), O(1)).
Độ phức tạp không gian (Space Complexity) là gì?;Là thước đo lượng bộ nhớ mà một thuật toán sử dụng dưới dạng một hàm của kích thước đầu vào (n). Cũng được biểu thị bằng ký hiệu Big O.
Big O Notation (O) đại diện cho điều gì?;Đại diện cho trường hợp tồi tệ nhất (worst-case). Nó mô tả cận trên của thời gian chạy hoặc không gian bộ nhớ mà thuật toán sẽ không bao giờ vượt qua.
Phân biệt O(1), O(log n), O(n), O(n²).;O(1): Hằng số (Constant) - Thời gian không đổi bất kể đầu vào.<br>O(log n): Logarit (Logarithmic) - Thời gian tăng chậm, thường liên quan đến việc chia đôi tập dữ liệu (chia để trị).<br>O(n): Tuyến tính (Linear) - Thời gian tăng tỷ lệ thuận với kích thước đầu vào.<br>O(n²): Bậc hai (Quadratic) - Thời gian tăng theo bình phương kích thước đầu vào (vòng lặp lồng nhau).
Cấu trúc dữ liệu (Data Structure) là gì?;Là một cách tổ chức, quản lý và lưu trữ dữ liệu trong máy tính để có thể được truy cập và sửa đổi một cách hiệu quả.
Phân biệt Cấu trúc dữ liệu tuyến tính và Phi tuyến tính.;Tuyến tính (Linear): Các phần tử được sắp xếp theo một trình tự tuần tự. Ví dụ: Mảng (Array), Danh sách liên kết (Linked List), Ngăn xếp (Stack), Hàng đợi (Queue).<br>Phi tuyến tính (Non-linear): Các phần tử không được sắp xếp tuần tự mà phân cấp. Ví dụ: Cây (Tree), Đồ thị (Graph).
Giải thuật (Algorithm) là gì?;Là một tập hợp hữu hạn các chỉ thị được định nghĩa rõ ràng, có thể thực hiện được bằng máy tính, để giải quyết một lớp các vấn đề hoặc để thực hiện một phép tính.
Đệ quy (Recursion) là gì?;Là một kỹ thuật lập trình trong đó một hàm tự gọi lại chính nó để giải quyết một phiên bản nhỏ hơn của cùng một vấn đề, cho đến khi đạt đến một trường hợp cơ sở (base case).
Mảng (Array);Một tập hợp các phần tử cùng kiểu dữ liệu, được lưu trữ tại các vị trí bộ nhớ liền kề.<br>Ưu điểm: Truy cập phần tử theo chỉ số (index) rất nhanh - O(1).<br>Nhược điểm: Kích thước cố định, chèn/xóa phần tử chậm - O(n).
Danh sách liên kết (Linked List);Một chuỗi các nút (node), mỗi nút chứa dữ liệu và một con trỏ đến nút tiếp theo.<br>Ưu điểm: Kích thước động, chèn/xóa phần tử nhanh (nếu đã có con trỏ) - O(1).<br>Nhược điểm: Truy cập phần tử chậm (phải duyệt từ đầu) - O(n).
Ngăn xếp (Stack);Một cấu trúc dữ liệu hoạt động theo nguyên tắc LIFO (Last-In, First-Out) - Vào sau, ra trước.<br>Các thao tác chính: `push` (thêm vào đỉnh), `pop` (lấy ra khỏi đỉnh).<br>Ứng dụng: Quản lý lời gọi hàm (call stack), nút Back trong trình duyệt.
Hàng đợi (Queue);Một cấu trúc dữ liệu hoạt động theo nguyên tắc FIFO (First-In, First-Out) - Vào trước, ra trước.<br>Các thao tác chính: `enqueue` (thêm vào cuối), `dequeue` (lấy ra khỏi đầu).<br>Ứng dụng: Quản lý tác vụ in, BFS trong đồ thị.
Danh sách liên kết đôi (Doubly Linked List);Một danh sách liên kết mà mỗi nút có hai con trỏ: một đến nút tiếp theo và một đến nút phía trước. Cho phép duyệt theo cả hai chiều.
Hàng đợi ưu tiên (Priority Queue);Một loại hàng đợi đặc biệt mà mỗi phần tử có một "độ ưu tiên". Phần tử có độ ưu tiên cao nhất sẽ được xử lý trước, bất kể thứ tự vào. Thường được triển khai bằng Heap.
Bảng băm (Hash Table);Một cấu trúc dữ liệu ánh xạ "khóa" (key) tới "giá trị" (value) bằng cách sử dụng một hàm băm (hash function).<br>Độ phức tạp trung bình: Chèn, xóa, tìm kiếm là O(1).<br>Xung đột (Collision): Xảy ra khi hai khóa khác nhau được băm ra cùng một chỉ số.
Hàm băm (Hash Function) là gì?;Là một hàm chuyển đổi một đầu vào (key) có kích thước bất kỳ thành một đầu ra (hash code) có kích thước cố định, thường là một chỉ số trong mảng của bảng băm.
Deque (Double-Ended Queue);Là một hàng đợi hai đầu. Cho phép thêm và xóa phần tử ở cả hai đầu (đầu và cuối) một cách hiệu quả - O(1).
Danh sách liên kết vòng (Circular Linked List);Là một danh sách liên kết mà nút cuối cùng trỏ trở lại nút đầu tiên, tạo thành một vòng tròn.
Cây (Tree);Một cấu trúc dữ liệu phân cấp bao gồm các nút được kết nối bằng các cạnh. Có một nút gốc (root) duy nhất và không có chu trình.
Cây nhị phân (Binary Tree);Một cây mà mỗi nút có tối đa hai nút con, thường được gọi là con trái (left child) và con phải (right child).
Cây tìm kiếm nhị phân (Binary Search Tree - BST);Một cây nhị phân có tính chất: Với mỗi nút, tất cả các giá trị trong cây con trái đều nhỏ hơn giá trị của nút đó, và tất cả các giá trị trong cây con phải đều lớn hơn.<br>Độ phức tạp trung bình: Tìm kiếm, chèn, xóa là O(log n).
Các phép duyệt cây: In-order, Pre-order, Post-order;In-order (Trung tự): Trái -> Gốc -> Phải (Duyệt BST theo thứ tự này sẽ cho ra dãy được sắp xếp).<br>Pre-order (Tiền tự): Gốc -> Trái -> Phải.<br>Post-order (Hậu tự): Trái -> Phải -> Gốc.
Cây cân bằng (Balanced Tree) (Ví dụ: Cây AVL, Cây Đỏ-Đen);Là một cây tìm kiếm nhị phân tự động giữ cho chiều cao của nó ở mức tối thiểu (cân bằng) sau mỗi lần chèn/xóa. Điều này đảm bảo độ phức tạp luôn là O(log n) trong trường hợp tồi tệ nhất.
Đống (Heap);Là một cấu trúc dữ liệu dạng cây nhị phân đặc biệt, thỏa mãn tính chất heap:<br>- Max-Heap: Giá trị của nút cha luôn lớn hơn hoặc bằng giá trị các nút con.<br>- Min-Heap: Giá trị của nút cha luôn nhỏ hơn hoặc bằng giá trị các nút con.<br>Ứng dụng: Heapsort, Hàng đợi ưu tiên.
Đồ thị (Graph);Một tập hợp các đỉnh (vertices/nodes) được kết nối với nhau bằng các cạnh (edges). Có thể có hướng (directed) hoặc vô hướng (undirected).
Duyệt đồ thị: BFS (Breadth-First Search);Tìm kiếm theo chiều rộng. Bắt đầu từ một đỉnh, duyệt tất cả các hàng xóm của nó, sau đó mới đến các hàng xóm của hàng xóm.<br>Sử dụng: Hàng đợi (Queue).<br>Ứng dụng: Tìm đường đi ngắn nhất trong đồ thị không có trọng số.
Duyệt đồ thị: DFS (Depth-First Search);Tìm kiếm theo chiều sâu. Bắt đầu từ một đỉnh, đi sâu nhất có thể theo một nhánh trước khi quay lui.<br>Sử dụng: Ngăn xếp (Stack) hoặc Đệ quy.<br>Ứng dụng: Phát hiện chu trình, sắp xếp topo.
Cây Trie (Prefix Tree);Một cấu trúc dữ liệu dạng cây dùng để lưu trữ và tìm kiếm một tập hợp các chuỗi một cách hiệu quả. Mỗi nút đại diện cho một ký tự. Rất hữu ích cho các tính năng tự động hoàn thành (autocomplete).
Sắp xếp nổi bọt (Bubble Sort);Lặp đi lặp lại việc so sánh hai phần tử liền kề và đổi chỗ chúng nếu chúng sai thứ tự.<br>Độ phức tạp: O(n²). Rất chậm và không hiệu quả.
Sắp xếp chèn (Insertion Sort);Xây dựng mảng đã sắp xếp một cách tuần tự. Lấy từng phần tử của mảng chưa sắp xếp và chèn nó vào đúng vị trí trong mảng đã sắp xếp.<br>Độ phức tạp: O(n²). Hiệu quả với các mảng nhỏ hoặc gần như đã được sắp xếp.
Sắp xếp trộn (Merge Sort);Một giải thuật Chia để trị (Divide and Conquer).<br>1. Chia: Liên tục chia mảng thành hai nửa cho đến khi mỗi mảng con chỉ còn một phần tử.<br>2. Trị: Trộn (merge) các mảng con đã sắp xếp lại với nhau.<br>Độ phức tạp: Luôn là O(n log n).
Sắp xếp nhanh (Quick Sort);Một giải thuật Chia để trị.<br>1. Chọn một phần tử làm "chốt" (pivot).<br>2. Phân hoạch (partition) mảng thành hai mảng con: một chứa các phần tử nhỏ hơn chốt, một chứa các phần tử lớn hơn chốt.<br>3. Đệ quy sắp xếp hai mảng con.<br>Độ phức tạp: Trung bình là O(n log n), tồi tệ nhất là O(n²).
Sắp xếp vun đống (Heap Sort);Sử dụng cấu trúc dữ liệu Đống (Heap).<br>1. Xây dựng một Max-Heap từ mảng đầu vào.<br>2. Lặp đi lặp lại việc lấy phần tử lớn nhất (ở gốc) và đặt nó vào cuối mảng, sau đó vun lại đống.<br>Độ phức tạp: Luôn là O(n log n).
Tìm kiếm tuyến tính (Linear Search);Duyệt qua từng phần tử của mảng từ đầu đến cuối để tìm một giá trị.<br>Độ phức tạp: O(n).
Tìm kiếm nhị phân (Binary Search);Một giải thuật tìm kiếm hiệu quả trên một mảng đã được sắp xếp.<br>1. So sánh giá trị cần tìm với phần tử ở giữa mảng.<br>2. Nếu khớp, trả về vị trí.<br>3. Nếu nhỏ hơn, tìm kiếm ở nửa bên trái. Nếu lớn hơn, tìm kiếm ở nửa bên phải.<br>Độ phức tạp: O(log n).
Giải thuật Dijkstra;Giải thuật tìm đường đi ngắn nhất từ một đỉnh nguồn đến tất cả các đỉnh khác trong một đồ thị có trọng số không âm. Sử dụng hàng đợi ưu tiên.
Giải thuật Bellman-Ford;Giải thuật tìm đường đi ngắn nhất từ một đỉnh nguồn, nhưng có khả năng xử lý các cạnh có trọng số âm và phát hiện chu trình âm.
Giải thuật Prim và Kruskal;Là hai giải thuật tham lam (greedy) dùng để tìm Cây khung nhỏ nhất (Minimum Spanning Tree - MST) trong một đồ thị vô hướng có trọng số.
Quy hoạch động (Dynamic Programming);Một kỹ thuật giải quyết các bài toán phức tạp bằng cách chia chúng thành các bài toán con đơn giản hơn, giải các bài toán con này (chỉ một lần) và lưu trữ kết quả của chúng để tránh tính toán lại.<br>Đặc điểm: Các bài toán con gối nhau (Overlapping Subproblems) và Cấu trúc con tối ưu (Optimal Substructure).
Giải thuật tham lam (Greedy Algorithm);Một giải thuật luôn đưa ra lựa chọn tối ưu cục bộ tại mỗi bước với hy vọng rằng những lựa chọn này sẽ dẫn đến một giải pháp tối ưu toàn cục. Không phải lúc nào cũng tìm được lời giải tối ưu.
```

Use code [with caution](https://support.google.com/legal/answer/13505487).

**Lưu ý:** Tôi đã thêm thẻ <br> vào một số câu trả lời để chúng có thể xuống dòng đẹp hơn khi hiển thị trong Anki.

1. **Lưu file** với một cái tên dễ nhớ, ví dụ: dsa_flashcards.txt. Hãy chắc chắn rằng bạn lưu nó với định dạng **UTF-8** để hiển thị đúng tiếng Việt.
    

---

### **Bước 2: Import vào Anki**

Bây giờ bạn đã có file dữ liệu, hãy mở chương trình Anki trên máy tính của bạn.

1. Từ cửa sổ chính của Anki, bấm vào nút **"Import File"** (Nhập tệp) ở phía dưới.
    
2. **Chọn file dsa_flashcards.txt** mà bạn vừa lưu.
    
3. Một cửa sổ "Import" sẽ hiện ra. Đây là bước quan trọng nhất để Anki hiểu đúng file của bạn.
    
    - **Type (Loại thẻ):** Chọn **"Basic"**. Đây là loại thẻ mặc định có 2 trường là "Front" và "Back".
        
    - **Deck (Bộ thẻ):** Chọn bộ thẻ mà bạn muốn thêm vào, hoặc bấm vào tên bộ thẻ để **tạo một bộ thẻ mới** (ví dụ: "CS - Data Structures & Algorithms").
        
    - **Fields separated by (Phân tách trường bởi):** Đây là lúc bạn cho Anki biết ký tự phân cách của bạn. Hãy chọn **"Semicolon" (Dấu chấm phẩy)**.
        
    - **Allow HTML in fields (Cho phép HTML trong các trường):** **Hãy đảm bảo ô này được tick ✅**. Điều này rất quan trọng để các thẻ <br> hoạt động và các câu trả lời của bạn được xuống dòng.
        
4. Bạn sẽ thấy một bản xem trước ở phía dưới. Cột "Field 1" sẽ là Mặt trước, và "Field 2" sẽ là Mặt sau. Nếu mọi thứ trông chính xác, hãy bấm nút **"Import"**.
    
5. Một thông báo sẽ hiện ra báo rằng "40 notes added" (Đã thêm 40 thẻ).
    

**Xong!** Bây giờ bạn có thể vào bộ thẻ mới của mình và bắt đầu học. Anki sẽ tự động sắp xếp lịch ôn tập để bạn có thể ghi nhớ kiến thức một cách hiệu quả nhất. Chúc bạn học tốt

---
---

Chắc chắn rồi! Dưới đây là 20 flashcard về các khái niệm cơ bản và quan trọng trong lĩnh vực Cơ sở dữ liệu (Database), đã được định dạng sẵn để bạn có thể dễ dàng import vào Anki.

---

### **Bước 1: Chuẩn bị file dữ liệu**

1. **Mở một trình soạn thảo văn bản** (Notepad, TextEdit, VSCode...).
    
2. **Sao chép (Copy)** toàn bộ nội dung trong khối code dưới đây.
    
3. **Dán (Paste)** vào file văn bản của bạn.
    
4. **Lưu file** với tên database_flashcards.txt và đảm bảo bạn chọn bảng mã **UTF-8** để hiển thị đúng tiếng Việt.
    

**Nội dung để copy:**

Generated code

```
Cơ sở dữ liệu (Database) là gì?;Là một tập hợp có tổ chức của các dữ liệu có cấu trúc, thường được lưu trữ và truy cập điện tử từ một hệ thống máy tính.
DBMS (Database Management System) là gì?;Là phần mềm hệ thống dùng để tạo, đọc, cập nhật và quản lý cơ sở dữ liệu. Ví dụ: MySQL, PostgreSQL, SQL Server, MongoDB.
SQL vs. NoSQL;<b>SQL (Relational Databases):</b><br>- Dữ liệu có cấu trúc, lưu trong các bảng (table).<br>- Schema cố định (strict schema).<br>- Thường scale theo chiều dọc (Vertical Scaling - nâng cấp phần cứng).<br>- Ví dụ: PostgreSQL, MySQL.<br><br><b>NoSQL (Non-relational Databases):</b><br>- Dữ liệu linh hoạt (có cấu trúc, bán cấu trúc, phi cấu trúc).<br>- Schema linh hoạt (dynamic schema).<br>- Thường scale theo chiều ngang (Horizontal Scaling - thêm máy chủ).<br>- Ví dụ: MongoDB, Redis.
Table, Row, và Column là gì?;Trong cơ sở dữ liệu quan hệ:<br>- <b>Table (Bảng):</b> Giống như một bảng tính Excel, chứa dữ liệu về một thực thể cụ thể (ví dụ: Bảng "SinhVien").<br>- <b>Row (Hàng) / Record:</b> Là một mục dữ liệu duy nhất trong bảng (ví dụ: thông tin của một sinh viên cụ thể).<br>- <b>Column (Cột) / Field:</b> Là một thuộc tính của thực thể (ví dụ: Cột "HoTen", "MaSV").
Khóa chính (Primary Key);Là một cột (hoặc tập hợp các cột) trong một bảng dùng để **xác định duy nhất** mỗi hàng. Giá trị của khóa chính không được phép rỗng (NULL) và phải là duy nhất.
Khóa ngoại (Foreign Key);Là một cột trong một bảng được dùng để liên kết đến khóa chính của một bảng khác. Nó tạo ra và thực thi một mối quan hệ giữa hai bảng.
SQL là viết tắt của gì?;<b>S</b>tructured <b>Q</b>uery <b>L</b>anguage (Ngôn ngữ truy vấn có cấu trúc). Đây là ngôn ngữ tiêu chuẩn để giao tiếp với cơ sở dữ liệu quan hệ.
DML (Data Manipulation Language);Là tập hợp các lệnh SQL dùng để **thao tác với dữ liệu**.<br>Bao gồm: `SELECT` (truy vấn), `INSERT` (thêm mới), `UPDATE` (cập nhật), và `DELETE` (xóa).
DDL (Data Definition Language);Là tập hợp các lệnh SQL dùng để **định nghĩa và quản lý cấu trúc** của cơ sở dữ liệu.<br>Bao gồm: `CREATE` (tạo bảng/database), `ALTER` (sửa đổi cấu trúc), và `DROP` (xóa bảng/database).
Truy vấn `SELECT`;Là lệnh SQL được sử dụng phổ biến nhất, dùng để truy xuất (lấy) dữ liệu từ một hoặc nhiều bảng.
Mệnh đề `JOIN`;Là một mệnh đề trong SQL dùng để kết hợp các hàng từ hai hoặc nhiều bảng dựa trên một cột có liên quan giữa chúng (thường là khóa ngoại và khóa chính).<br>Loại phổ biến nhất là `INNER JOIN`, trả về các hàng có giá trị khớp ở cả hai bảng.
Chỉ mục (Index);Là một cấu trúc dữ liệu đặc biệt giúp tăng tốc độ truy vấn dữ liệu trong database. Nó hoạt động giống như mục lục của một cuốn sách, cho phép DBMS tìm thấy dữ liệu nhanh hơn mà không cần phải quét toàn bộ bảng.
Giao dịch (Transaction);Là một chuỗi các thao tác được thực hiện như một đơn vị logic công việc duy nhất. Một giao dịch hoặc là **thành công toàn bộ** (commit) hoặc là **thất bại toàn bộ** (rollback), không có trạng thái lưng chừng.
Thuộc tính ACID;Là bốn thuộc tính đảm bảo tính tin cậy của các giao dịch trong database:<br><b>A</b>tomicity (Tính nguyên tử): Hoặc tất cả các thao tác đều thành công, hoặc không có gì cả.<br><b>C</b>onsistency (Tính nhất quán): Dữ liệu luôn ở trạng thái hợp lệ trước và sau giao dịch.<br><b>I</b>solation (Tính cô lập): Các giao dịch đồng thời không ảnh hưởng lẫn nhau.<br><b>D</b>urability (Tính bền vững): Một khi giao dịch đã được commit, nó sẽ tồn tại vĩnh viễn, ngay cả khi hệ thống gặp sự cố.
Chuẩn hóa (Normalization);Là quá trình thiết kế cơ sở dữ liệu quan hệ để giảm thiểu sự dư thừa dữ liệu và cải thiện tính toàn vẹn dữ liệu. Nó bao gồm việc chia các bảng lớn thành các bảng nhỏ hơn và được tổ chức tốt hơn.
Phi chuẩn hóa (Denormalization);Là quá trình cố tình thêm dữ liệu dư thừa vào một hoặc nhiều bảng. Mục đích là để **tăng tốc độ truy vấn** bằng cách tránh các phép `JOIN` phức tạp, thường được áp dụng trong các hệ thống cần đọc dữ liệu nhanh.
Các loại cơ sở dữ liệu NoSQL;Có 4 loại chính:<br>1. <b>Document Databases:</b> Lưu dữ liệu dưới dạng tài liệu (JSON, BSON). Ví dụ: MongoDB.<br>2. <b>Key-Value Stores:</b> Lưu dữ liệu dưới dạng cặp khóa-giá trị đơn giản. Ví dụ: Redis.<br>3. <b>Column-Family Stores:</b> Lưu dữ liệu theo cột thay vì theo hàng. Tối ưu cho việc tổng hợp dữ liệu lớn. Ví dụ: Cassandra.<br>4. <b>Graph Databases:</b> Lưu dữ liệu dưới dạng các đỉnh và cạnh. Tối ưu cho việc truy vấn các mối quan hệ phức tạp. Ví dụ: Neo4j.
Định lý CAP (CAP Theorem);Một định lý cơ bản trong khoa học máy tính cho các hệ thống phân tán (distributed systems). Nó phát biểu rằng một hệ thống chỉ có thể đảm bảo **tối đa hai** trong ba thuộc tính sau:<br>- <b>C</b>onsistency (Tính nhất quán)<br>- <b>A</b>vailability (Tính sẵn sàng)<br>- <b>P</b>artition Tolerance (Khả năng chịu lỗi phân mảnh)
Khung nhìn (View);Là một bảng ảo dựa trên kết quả của một câu lệnh `SELECT`. Một View chứa các hàng và cột giống như một bảng thật. Nó có thể được dùng để đơn giản hóa các truy vấn phức tạp, hạn chế quyền truy cập dữ liệu, hoặc tóm tắt dữ liệu.
Thủ tục lưu trữ (Stored Procedure);Là một tập hợp các câu lệnh SQL đã được biên dịch trước và được lưu trữ trong cơ sở dữ liệu. Thay vì gửi nhiều lệnh SQL riêng lẻ, ứng dụng có thể gọi thực thi thủ tục này chỉ bằng một lệnh gọi, giúp giảm lưu lượng mạng và tăng tính bảo mật.
```

Use code [with caution](https://support.google.com/legal/answer/13505487).

---

### **Bước 2: Import vào Anki**

1. Mở chương trình Anki trên máy tính của bạn.
    
2. Bấm vào nút **"Import File"** (Nhập tệp).
    
3. **Chọn file database_flashcards.txt** mà bạn vừa lưu.
    
4. Trong cửa sổ "Import" hiện ra:
    
    - **Type (Loại thẻ):** Chọn **"Basic"**.
        
    - **Deck (Bộ thẻ):** Chọn một bộ thẻ có sẵn hoặc tạo bộ thẻ mới (ví dụ: "IT - Database Concepts").
        
    - **Fields separated by (Phân tách trường bởi):** Chọn **"Semicolon" (Dấu chấm phẩy)**.
        
    - **Allow HTML in fields (Cho phép HTML trong các trường):** **Đảm bảo ô này được tick ✅** để các thẻ <br> và <b> hoạt động.
        
5. Kiểm tra bản xem trước để đảm bảo "Field 1" là Mặt trước và "Field 2" là Mặt sau.
    
6. Bấm nút **"Import"**.
    

Vậy là xong! Bạn đã có một bộ flashcard chất lượng về Database để bắt đầu ôn tập. Chúc bạn học tốt