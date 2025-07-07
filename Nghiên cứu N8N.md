![[Nghiên cứu N8N.png]]Ok, hãy hình dung đơn giản hơn nhé.

Đây là một quy trình tự động, giống như một người giúp việc thông minh, làm các việc sau khi bạn yêu cầu tạo một người dùng mới trong công ty:

1. **Bước 1: "Có ai đó muốn tạo tài khoản mới!"**
    
    - Giống như có người điền vào một tờ giấy "Đề nghị tạo tài khoản mới" và nhấn nút gửi. Đây là lúc mọi thứ bắt đầu.
        
2. **Bước 2: "Người giúp việc AI thông minh bắt đầu làm việc."**
    
    - Người giúp việc này không phải người bình thường mà là một AI (trí tuệ nhân tạo).
        
    - Nó có một "bộ não" để nói chuyện/hiểu yêu cầu của bạn (nhờ **Anthropic Chat Model**).
        
    - Nó có một "quyển sổ ghi nhớ" để nhớ những gì đã làm trước đây hoặc thông tin về người đó (**Postgres Chat Memory**).
        
    - Và quan trọng nhất, nó có "các công cụ" để làm việc:
        
        - Một công cụ để **tìm thông tin người dùng trong hệ thống Microsoft Entra ID** (giống như xem trong danh bạ công ty).
            
        - Một công cụ để **tạo tài khoản mới trong Jira Software** (Jira là một phần mềm quản lý công việc).
            
3. **Bước 3: "Người này có phải là sếp không?"**
    
    - Sau khi người giúp việc AI đã xử lý thông tin, nó tự hỏi: "À, người này mình vừa tạo là quản lý hay nhân viên bình thường nhỉ?"
        
4. **Bước 4a: "Nếu là sếp..."**
    
    - Nếu câu trả lời là "Đúng, là sếp!", thì người giúp việc sẽ tự động **thêm người đó vào một kênh chat đặc biệt dành cho các sếp** (ví dụ, một nhóm chat Slack chỉ dành cho quản lý).
        
5. **Bước 4b: "Nếu không phải là sếp..."**
    
    - Nếu câu trả lời là "Không, chỉ là nhân viên bình thường!", thì người giúp việc sẽ tự động **cập nhật thông tin cá nhân của người đó** trong hệ thống (ví dụ, cập nhật hồ sơ của họ trên Slack).
        

**Tóm lại:**

Đây là một hệ thống tự động giúp bạn **tạo tài khoản mới cho nhân viên/quản lý**. Nó dùng AI để hiểu yêu cầu, dùng các phần mềm khác để tạo tài khoản, và tự động quyết định xem người đó là sếp hay không để đưa họ vào đúng nhóm chat hoặc cập nhật thông tin cho phù hợp. Mọi thứ diễn ra tự động mà không cần con người can thiệp nhiều sau khi yêu cầu được gửi đi.


---
![[Nghiên cứu N8N-2.png]]