# Phân Tích Kiến Trúc và Mã Nguồn cho Phần Mềm Quản Lý Xưởng Sản Xuất Số Hóa

## Lời Mở Đầu: Chuyển Đổi Số tại Tầng Sản Xuất

### Bối Cảnh: Từ Sản Xuất Truyền Thống đến Công Nghiệp 4.0

Quá trình chuyển đổi từ sản xuất truyền thống sang Công nghiệp 4.0 đang định hình lại toàn bộ ngành công nghiệp. Cốt lõi của cuộc cách mạng này là sự tích hợp liền mạch giữa thế giới vật lý và thế giới số, nơi dữ liệu trở thành tài sản chiến lược. Phần mềm quản lý đóng vai trò trung tâm trong việc kết nối các hệ thống lập kế hoạch cấp doanh nghiệp (ERP) với các hoạt động vận hành thực tế tại xưởng sản xuất (shop floor). Sự kết nối này là nền tảng của tiêu chuẩn ISA-95, một khuôn khổ quốc tế nhằm tích hợp hệ thống doanh nghiệp với hoạt động sản xuất. Các Hệ thống Điều hành Sản xuất (Manufacturing Execution Systems - MES) nổi lên như một giải pháp quan trọng để lấp đầy khoảng trống này, cho phép theo dõi thời gian thực, kiểm soát sản xuất, truy xuất nguồn gốc và phân tích hiệu suất.  

### Lợi Thế của Nguồn Mở

Trong bối cảnh chi phí và sự phức tạp của các giải pháp MES độc quyền có thể là rào cản lớn, đặc biệt đối với các doanh nghiệp vừa và nhỏ (SMEs), phần mềm nguồn mở nổi lên như một lựa chọn chiến lược. Các nền tảng nguồn mở mang lại nhiều lợi ích đáng kể: giảm chi phí đầu vào, tăng cường tính minh bạch, và quan trọng nhất là khả năng tùy chỉnh sâu rộng để phù hợp với các quy trình sản xuất độc nhất, đồng thời tránh được sự phụ thuộc vào nhà cung cấp (vendor lock-in). Việc tiếp cận toàn bộ mã nguồn cho phép các doanh nghiệp không chỉ điều chỉnh phần mềm mà còn tích hợp nó một cách chặt chẽ vào hệ sinh thái công nghệ thông tin hiện có.  

### Phương Pháp Luận

Báo cáo này cung cấp một phân tích kỹ thuật sâu rộng về kiến trúc và các ví dụ mã nguồn của các phần mềm quản lý sản xuất số hóa nguồn mở hàng đầu. Báo cáo được cấu trúc để đi từ phân tích kiến trúc cấp cao, so sánh các triết lý thiết kế nền tảng, đến việc triển khai các chức năng quan trọng ở cấp độ mã nguồn. Cuối cùng, báo cáo sẽ đưa ra một khung chiến lược để hỗ trợ các kiến trúc sư giải pháp và các nhà phát triển trong việc lựa chọn và triển khai hệ thống phù hợp nhất.

## Phần 1: Phân Tích So Sánh Kiến Trúc các Nền Tảng Sản Xuất Nguồn Mở

Phần này cung cấp một cái nhìn tổng quan chiến lược về bối cảnh kiến trúc phần mềm, cho phép người đọc hiểu rõ các triết lý thiết kế cơ bản của các hệ thống khác nhau trước khi đi sâu vào chi tiết mã nguồn.

### 1.1 Phổ Kiến Trúc: Từ ERP Nguyên Khối đến MES API-First

#### Mô Hình ISA-95 như một Kim Chỉ Nam Kiến Trúc

Để đánh giá một kiến trúc phần mềm sản xuất, việc tham chiếu đến mô hình kim tự tháp tự động hóa ANSI/ISA-95 là vô cùng hữu ích. Mô hình này phân tầng hệ thống sản xuất từ cấp độ quy trình vật lý (Cấp 0) đến cấp độ doanh nghiệp (Cấp 4). Hệ thống MES nằm ở Cấp 3, một vị trí chiến lược, đóng vai trò là cầu nối quan trọng giữa hệ thống ERP (Cấp 4) và hệ thống điều khiển tầng sản xuất (Cấp 1-2). Việc một hệ thống phần mềm được thiết kế để phục vụ tốt vai trò này hay không phụ thuộc rất nhiều vào kiến trúc nền tảng của nó.  

#### Kiến Trúc Nguyên Khối (Monolithic)

Kiến trúc nguyên khối được đặc trưng bởi các mô-đun chức năng được tích hợp chặt chẽ trong một ứng dụng duy nhất, thống nhất. Ưu điểm của phương pháp này bao gồm tính nhất quán cao trong toàn bộ hệ thống và việc triển khai ban đầu tương đối đơn giản. Tuy nhiên, nó cũng đi kèm với những thách thức về khả năng mở rộng và sự cứng nhắc về công nghệ khi cần thay đổi hoặc nâng cấp. Các hệ thống ERP toàn diện như ERPNext, được xây dựng trên Frappe Framework "full-stack" , và Odoo, với bộ ứng dụng tích hợp của nó , là những ví dụ điển hình cho phong cách kiến trúc trưởng thành này. Chúng cung cấp một giải pháp "tất cả trong một" mạnh mẽ, nơi các chức năng từ kế toán, nhân sự đến sản xuất đều được quản lý trong một nền tảng duy nhất.  

#### Kiến Trúc API-First và Mô-đun Hóa

Trái ngược với kiến trúc nguyên khối, kiến trúc API-First (ưu tiên API) và mô-đun hóa tập trung vào việc xây dựng một hệ thống lõi tinh gọn, phơi bày các chức năng của nó thông qua các giao diện lập trình ứng dụng (API) được định nghĩa rõ ràng. Cách tiếp cận này ưu tiên khả năng mở rộng và tích hợp, cho phép các nhà phát triển xây dựng các ứng dụng độc lập hoặc các microservice tùy chỉnh trên nền tảng lõi. Carbon là một ví dụ hiện đại về triết lý này, được thiết kế rõ ràng để giải quyết vấn đề phụ thuộc vào nhà cung cấp và thực tế rằng "không có ERP hoàn hảo" bằng cách giúp người dùng dễ dàng xây dựng các ứng dụng của riêng họ. Tương tự, iPlus-MES cũng nhấn mạnh "tính mở và khả năng mở rộng thực sự" thông qua việc kế thừa và phát triển các thành phần mới.  

Việc lựa chọn giữa hai trường phái kiến trúc này không chỉ là một quyết định kỹ thuật đơn thuần mà còn là một quyết định chiến lược về phát triển phần mềm. Một hệ thống nguyên khối như ERPNext có thể yêu cầu chuyên môn sâu về một framework cụ thể (ví dụ: Frappe) để tùy chỉnh, trong khi một hệ thống API-first như Carbon đòi hỏi một đội ngũ có kỹ năng xây dựng và tích hợp các ứng dụng phân tán. Do đó, việc hiểu rõ triết lý kiến trúc của một nền tảng là bước đầu tiên và quan trọng nhất để xác định xem nó có phù hợp với chiến lược công nghệ và nguồn lực của tổ chức hay không.

### 1.2 Phân Tích Sâu: Các "Gã Khổng Lồ" Lấy ERP làm Trung Tâm (ERPNext & Odoo)

#### ERPNext (Frappe Framework)

- **Kiến trúc:** ERPNext được xây dựng trên Frappe Framework, một framework ứng dụng web full-stack, hướng siêu dữ liệu (metadata-driven) sử dụng Python và MariaDB. Khái niệm "DocType" của framework này đóng vai trò là khối xây dựng cơ bản cho tất cả các mô-đun, bao gồm Sản xuất (Manufacturing), Kho (Stock), và Quản lý Đơn hàng (Order Management). Cấu trúc này cho phép tùy chỉnh và mở rộng hệ thống một cách nhất quán.  
    
- **Năng lực Sản xuất:** ERPNext cung cấp một mô-đun sản xuất toàn diện giúp đơn giản hóa chu trình sản xuất, theo dõi tiêu thụ nguyên vật liệu, lập kế hoạch năng lực và quản lý gia công ngoài. Nó được định vị là một hệ thống ERP 100% nguồn mở theo giấy phép GPL-3.0.  
    
- **Cộng đồng & Hệ sinh thái:** Dự án tự hào có một cộng đồng lớn mạnh với 28,2 nghìn sao và 9,3 nghìn fork trên GitHub, cho thấy sự chấp nhận rộng rãi và hỗ trợ mạnh mẽ từ cộng đồng.  
    

#### Odoo

- **Kiến trúc:** Odoo được trình bày như một bộ ứng dụng kinh doanh nguồn mở dựa trên web. Kiến trúc của nó có tính mô-đun hóa cao, cho phép người dùng cài đặt các ứng dụng (ví dụ: Sản xuất, Tồn kho, CRM) theo nhu cầu. Backend chủ yếu được xây dựng bằng Python và cơ sở dữ liệu PostgreSQL.  
    
- **Năng lực Sản xuất:** Nền tảng này bao gồm một mô-đun Sản xuất mạnh mẽ, tích hợp liền mạch với các ứng dụng khác như Tồn kho và Quản lý Kho. Hiệp hội Cộng đồng Odoo (Odoo Community Association - OCA) cung cấp một kho lưu trữ khổng lồ các addon bổ sung liên quan đến sản xuất, mở rộng đáng kể chức năng của hệ thống.  
    
- **Cộng đồng & Hệ sinh thái:** Odoo là dự án phổ biến nhất trong danh mục này, với 45,6 nghìn sao và 29,5 nghìn fork, phản ánh sự thống trị thị trường và một cộng đồng vô cùng rộng lớn. Phiên bản cộng đồng của nó hoạt động theo giấy phép LGPLv3.  
    

### 1.3 Phân Tích Sâu: Các Nền Tảng MES Chuyên Dụng, Hiện Đại

#### Carbon

- **Kiến trúc:** Carbon là một monorepo hiện đại, theo triết lý API-first, được xây dựng bằng TypeScript và sử dụng Turborepo để quản lý. Nó được thiết kế rõ ràng cho khả năng mở rộng, cho phép người dùng xây dựng các ứng dụng của riêng họ. Kiến trúc này nhấn mạnh vào an toàn kiểu dữ liệu toàn diện (full-stack type safety), đăng ký cơ sở dữ liệu thời gian thực (real-time database subscriptions), và các tính năng bảo mật mạnh mẽ như Kiểm soát truy cập dựa trên thuộc tính (ABAC) và Bảo mật cấp hàng (RLS).  
    
- **Trường hợp sử dụng mục tiêu:** Hoàn hảo cho các quy trình sản xuất lắp ráp phức tạp, sản xuất đa dạng sản phẩm với số lượng thấp (High-Mix Low-Volume - HMLV), và sản xuất theo đơn đặt hàng cấu hình (configure-to-order).  
    
- **Mô hình cấp phép:** Sử dụng giấy phép AGPLv3 cho các kho lưu trữ công khai, và yêu cầu giấy phép thương mại cho việc sử dụng riêng tư. Đây là một mô hình phổ biến cho các doanh nghiệp nguồn mở hiện đại.  
    

#### iPlus-MES

- **Kiến trúc:** Được xây dựng trên iPlus-framework của.NET, iPlus-MES là một hệ thống MES có khả năng cấu hình và thích ứng cao, được thiết kế để hợp nhất các chức năng của SCADA và MES. Hệ thống sử dụng cơ sở dữ liệu Microsoft SQL Server.  
    
- **Tính năng chính:** Cung cấp các mô-đun toàn diện cho Dữ liệu Chủ (Master Data), Sản xuất, Quản lý Vật liệu, Logistics, Quản lý Chất lượng và Bảo trì. Dự án nhấn mạnh sự thành công đã được chứng minh với hơn 30 lượt cài đặt và hơn 4000 máy móc được kết nối.  
    
- **Điểm độc đáo:** Hiện tại, nó có thể chạy trên Linux/Android thông qua WINE, với kế hoạch hỗ trợ gốc trong tương lai bằng Avalonia XPF. Nó cũng có một mô hình chia sẻ doanh thu độc đáo cho những người đóng góp.  
    

#### qcadoo MES

- **Kiến trúc:** Một ứng dụng web để quản lý sản xuất được xây dựng bằng Java và PLpgSQL.  
    
- **Đối tượng mục tiêu:** Nhắm mục tiêu cụ thể đến các công ty vừa và nhỏ (SMEs).  
    
- **Mô hình cấp phép:** Có sự phân chia rõ ràng giữa phiên bản Cộng đồng (Community) và Thương mại (Commercial). Phiên bản cộng đồng nguồn mở có sẵn trên GitHub, trong khi phiên bản thương mại cung cấp hỗ trợ đầy đủ, triển khai SaaS, API REST và các mô-đun bổ sung. Mô hình "freemium" này là một chiến lược phổ biến để cân bằng giữa việc thu hút cộng đồng và đảm bảo tính bền vững thương mại.  
    

#### mes4u

- **Kiến trúc:** Một hệ thống MES nguồn mở dựa trên web do Sindoh phát triển, dựa trên hệ thống nội bộ của họ. Backend sử dụng Spring Boot (Java) và PostgreSQL, trong khi frontend được xây dựng bằng Vue.js.  
    
- **Phạm vi:** Phiên bản hiện tại cung cấp các chức năng cốt lõi và dữ liệu chủ, với kế hoạch bổ sung các tính năng quản lý tồn kho và vật liệu. Điều này cho thấy dự án đang ở giai đoạn phát triển tương đối sớm nhưng có định hướng rõ ràng.  
    

### Bảng 1: Ma Trận So Sánh các Nền Tảng Nguồn Mở Hàng Đầu

Bảng dưới đây cung cấp một cái nhìn tổng quan, so sánh các thuộc tính kỹ thuật và kinh doanh quan trọng của các nền tảng được phân tích, giúp các nhà ra quyết định nhanh chóng đánh giá và lựa chọn giải pháp phù hợp.

|Nền tảng|Ngăn xếp Công nghệ Chính|Phong cách Kiến trúc|Giấy phép|Mô-đun Sản xuất Chính|Sức khỏe Cộng đồng (Sao/Fork GitHub)|
|---|---|---|---|---|---|
|**ERPNext**|Python, MariaDB, JavaScript (Vue.js)|Nguyên khối (Monolithic) trên Frappe Framework|GPL-3.0|Sản xuất, Tồn kho, Quản lý đơn hàng, Kế toán|28.2k / 9.3k|
|**Odoo**|Python, PostgreSQL, JavaScript|Mô-đun hóa, Tích hợp|LGPL-3.0 (Community)|Sản xuất, Tồn kho, PLM, Bảo trì, Chất lượng|45.6k / 29.5k|
|**Carbon**|TypeScript, PLpgSQL, Docker|API-First, Monorepo|AGPL-3.0 / Thương mại|Lắp ráp phức tạp, HMLV, CTO|1.4k / 114|
|**iPlus-MES**|.NET Framework, C#, MS SQL Server|Cấu hình cao, Mở rộng|GPL-3.0 (với ngoại lệ)|Dữ liệu chủ, Sản xuất & Điều khiển, Quản lý vật liệu, Chất lượng, Bảo trì|N/A (Mã nguồn mới công khai)|
|**qcadoo MES**|Java, PLpgSQL, JavaScript|Dựa trên web, Hướng SME|AGPL-3.0 (Community)|Quản lý sản xuất, Lập kế hoạch, Theo dõi đơn hàng|834 / 439|
|**mes4u**|Java (Spring Boot), PostgreSQL, Vue.js|Dựa trên web, Hướng chức năng lõi|LGPL-2.1|Dữ liệu chủ, Chức năng sản xuất cốt lõi|44 / 13|

## Phần 2: Triển Khai Chức Năng Sản Xuất Quan Trọng ở Cấp Độ Mã Nguồn

Phần này chuyển từ kiến trúc cấp cao sang triển khai thực tế, cung cấp các ví dụ mã nguồn được chú thích chi tiết cho các chức năng cốt lõi của phần mềm sản xuất.

### 2.1 Lập Kế Hoạch Sản Xuất Nâng Cao: Từ Lý Thuyết đến Mã Nguồn

#### Thách Thức: Bài Toán Lập Lịch Phân Xưởng (JSSP)

Bài toán Lập lịch Phân xưởng (Job Shop Scheduling Problem - JSSP) là một bài toán tối ưu hóa kinh điển thuộc lớp NP-khó trong lĩnh vực sản xuất. Bài toán này yêu cầu sắp xếp lịch trình cho `n` công việc (jobs) trên `m` máy móc (machines), trong đó mỗi công việc có một chuỗi các công đoạn (tasks) phải được thực hiện theo một trình tự nhất định trên các máy cụ thể. Độ phức tạp của JSSP là lý do tại sao các hệ thống ERP thông thường thường chỉ cung cấp các công cụ lập kế hoạch cơ bản thay vì các giải pháp tối ưu hóa thực sự.  

#### Các Phương Pháp Tiếp Cận Thuật Toán

- **Heuristics và Thực Tiễn Tốt Nhất (frePPLe):** Một cách tiếp cận thực tế là sử dụng các thuật toán dựa trên kiến thức chuyên ngành sâu rộng. `frePPLe`, một công cụ Lập kế hoạch và Lịch trình Nâng cao (Advanced Planning and Scheduling - APS) nguồn mở, là một ví dụ điển hình. Nó triển khai các thuật toán dựa trên các lý thuyết sản xuất đã được kiểm chứng như Lý thuyết về các điểm hạn chế (Theory of Constraints - lập kế hoạch xoay quanh các điểm nghẽn cổ chai), lập kế hoạch dựa trên lực kéo (pull-based planning - bắt đầu sản xuất muộn nhất có thể và được kích hoạt trực tiếp bởi nhu cầu), và sản xuất tinh gọn (lean manufacturing - tránh tồn kho và sự chậm trễ trung gian).  
    
- **Metaheuristics (Thuật Toán Di Truyền):** Đối với các bài toán tối ưu hóa phức tạp như JSSP, các thuật toán metaheuristic như Thuật toán Di truyền (Genetic Algorithm - GA) cung cấp một phương pháp mạnh mẽ và linh hoạt. GA mô phỏng quá trình chọn lọc tự nhiên để tìm kiếm các giải pháp tối ưu hoặc gần tối ưu. Nhiều dự án nguồn mở bằng Python đã chứng minh tính hiệu quả của phương pháp này cho JSSP.  
    

#### Phân Tích Sâu Mã Nguồn: Thuật Toán Di Truyền bằng Python cho JSSP

Dưới đây là phân tích một ví dụ triển khai thuật toán di truyền bằng Python để giải quyết bài toán JSSP, dựa trên các ví dụ mã nguồn được tìm thấy.  

- **Khởi tạo Quần thể (Population Initialization):** Quá trình bắt đầu bằng việc tạo ra một quần thể ban đầu gồm các "cá thể" (individuals), mỗi cá thể là một "nhiễm sắc thể" (chromosome) đại diện cho một lịch trình sản xuất tiềm năng. Các lịch trình này thường được tạo ra một cách ngẫu nhiên, đảm bảo tính đa dạng cho quá trình tìm kiếm.  
    
- **Tính toán Độ thích nghi (Fitness Calculation):** Mỗi lịch trình trong quần thể được đánh giá bằng một "hàm thích nghi" (fitness function). Trong JSSP, độ thích nghi thường được đo bằng "makespan" - tổng thời gian cần thiết để hoàn thành tất cả các công việc. Mục tiêu của thuật toán là tìm ra lịch trình có makespan nhỏ nhất, tức là độ thích nghi cao nhất.  
    
- **Chọn lọc (Selection):** Các cá thể có độ thích nghi cao hơn sẽ có xác suất được chọn để "sinh sản" cao hơn. Quá trình này mô phỏng nguyên tắc "kẻ mạnh nhất sống sót" trong tự nhiên, đảm bảo rằng các đặc tính tốt của các lịch trình hiệu quả sẽ được truyền lại cho thế hệ sau.
    
- **Lai ghép (Crossover):** Hai cá thể "cha mẹ" được chọn sẽ trao đổi một phần thông tin di truyền (các đoạn của lịch trình) để tạo ra các cá thể "con" mới. Phép toán lai ghép hai điểm (two-point crossover) là một kỹ thuật phổ biến, trong đó một đoạn giữa hai điểm cắt ngẫu nhiên của nhiễm sắc thể cha mẹ được trao đổi với nhau. Một bước quan trọng sau lai ghép là "sửa chữa" (repairment) để đảm bảo rằng các lịch trình con mới tạo ra vẫn hợp lệ (ví dụ: mỗi công việc vẫn có đủ số lượng công đoạn cần thiết).  
    
- **Đột biến (Mutation):** Để duy trì sự đa dạng di truyền và tránh bị mắc kẹt tại các điểm tối ưu cục bộ (local optima), một tỷ lệ nhỏ các cá thể con sẽ trải qua quá trình đột biến. Đột biến thực hiện những thay đổi ngẫu nhiên nhỏ trong lịch trình, chẳng hạn như hoán vị vị trí của hai công đoạn.  
    
- **Lặp lại và Hội tụ:** Toàn bộ chu trình chọn lọc, lai ghép và đột biến được lặp lại qua nhiều thế hệ. Qua mỗi thế hệ, độ thích nghi trung bình của quần thể có xu hướng tăng lên, và thuật toán sẽ dần hội tụ về một giải pháp tối ưu hoặc gần tối ưu cho bài toán JSSP.  
    

Một thực tế quan trọng trong ngành là việc lập kế hoạch sản xuất tối ưu là một lĩnh vực chuyên biệt. Độ phức tạp toán học của các bài toán như JSSP có nghĩa là chúng thường được giải quyết bởi các công cụ hoặc thư viện chuyên dụng, thay vì là một tính năng cốt lõi của một hệ thống ERP giao dịch. Một hệ thống ERP quản lý các lệnh sản xuất và tồn kho; một công cụ lập lịch tối ưu hóa trình tự và thời gian thực hiện chúng. Do đó, một giải pháp sản xuất toàn diện thường đòi hỏi một cách tiếp cận "kết hợp những gì tốt nhất" (best-of-breed), tích hợp ERP/MES với một công cụ lập lịch chuyên dụng. Chất lượng API của hệ thống ERP/MES để xuất dữ liệu sản xuất và nhập lại lịch trình đã được tối ưu hóa trở thành một tiêu chí đánh giá cực kỳ quan trọng, như được đề xuất trong chiến lược "phân lớp mô-đun".  

### 2.2 Tích Hợp Dữ Liệu Tầng Sản Xuất với Giao Thức IIoT

#### Cầu Nối đến Thế Giới Vật Lý

Phần này tập trung vào nhiệm vụ thu thập dữ liệu thời gian thực từ máy móc, cảm biến và các bộ điều khiển logic khả trình (PLC) tại xưởng sản xuất. Đây là nền tảng của nhà máy số, cho phép giám sát và ra quyết định dựa trên dữ liệu thực tế.

#### So Sánh Giao Thức: MQTT và OPC-UA

Hai giao thức truyền thông chiếm ưu thế trong lĩnh vực Internet vạn vật công nghiệp (IIoT) là MQTT và OPC-UA. Việc lựa chọn giao thức phù hợp phụ thuộc vào yêu cầu cụ thể của ứng dụng.

- **MQTT (Message Queuing Telemetry Transport):** Là một giao thức nhắn tin theo mô hình publish-subscribe (xuất bản-đăng ký) cực kỳ nhẹ, được thiết kế cho việc truyền dữ liệu đo từ xa (telemetry) từ các thiết bị có tài nguyên hạn chế. MQTT hoạt động dựa trên một máy chủ trung tâm gọi là "broker" để điều phối tin nhắn giữa các thiết bị.  
    
- **OPC-UA (Open Platform Communications Unified Architecture):** Là một tiêu chuẩn truyền thông toàn diện, an toàn và hướng dịch vụ cho tự động hóa công nghiệp. OPC-UA cung cấp một mô hình dữ liệu phong phú, cho phép mô tả ngữ nghĩa của dữ liệu, và thường được tích hợp sẵn vào các PLC hiện đại. Nó không chỉ truyền dữ liệu mà còn cung cấp các dịch vụ như gọi phương thức, cảnh báo và sự kiện.  
    

Bảng dưới đây so sánh các đặc tính kỹ thuật chính của hai giao thức này để hỗ trợ việc ra quyết định kiến trúc.

### Bảng 2: So Sánh Giao Thức IIoT cho Thu Thập Dữ Liệu Tầng Sản Xuất

|Đặc tính|MQTT|OPC-UA|
|---|---|---|
|**Giao thức Vận chuyển**|TCP/IP|TCP/IP, WebSockets|
|**Mô hình Dữ liệu**|Tải trọng (payload) dữ liệu tùy ý, không có cấu trúc|Mô hình đối tượng có cấu trúc, phong phú về ngữ nghĩa|
|**Bảo mật**|TLS, Tên người dùng/Mật khẩu|Tích hợp sâu: x.509 certificates, mã hóa, ký số, xác thực người dùng|
|**Mô hình Giao tiếp**|Publish/Subscribe|Client/Server, Publish/Subscribe|
|**Trường hợp Sử dụng**|Đo từ xa từ cảm biến đơn giản, mạng không ổn định, băng thông thấp|Điều khiển máy móc phức tạp, tích hợp PLC, yêu cầu bảo mật cao, ngữ cảnh hóa dữ liệu|

Xuất sang Trang tính

#### Phân Tích Sâu Mã Nguồn: Python MQTT Publisher

Dưới đây là ví dụ mã nguồn và phân tích chi tiết một client MQTT bằng Python sử dụng thư viện `paho-mqtt` để xuất bản dữ liệu lên một broker.  

Python

```
# python 3.11
import random
import time
from paho.mqtt import client as mqtt_client

broker = 'broker.emqx.io'
port = 1883
topic = "python/mqtt"
client_id = f'publish-{random.randint(0, 1000)}'

def connect_mqtt():
    def on_connect(client, userdata, flags, rc):
        if rc == 0:
            print("Connected to MQTT Broker!")
        else:
            print(f"Failed to connect, return code {rc}\n")

    client = mqtt_client.Client(client_id)
    client.on_connect = on_connect
    client.connect(broker, port)
    return client

def publish(client):
    msg_count = 0
    while True:
        time.sleep(1)
        msg = f"messages: {msg_count}"
        result = client.publish(topic, msg)
        status = result
        if status == 0:
            print(f"Send `{msg}` to topic `{topic}`")
        else:
            print(f"Failed to send message to topic {topic}")
        msg_count += 1
        if msg_count > 5:
            break

def run():
    client = connect_mqtt()
    client.loop_start()
    publish(client)
    client.loop_stop()

if __name__ == '__main__':
    run()
```

**Phân tích mã nguồn:**

1. **Thiết lập kết nối:** Hàm `connect_mqtt` khởi tạo một đối tượng `mqtt_client.Client` với một `client_id` duy nhất. Nó gán một hàm callback  
    
    `on_connect` để xử lý kết quả kết nối và sau đó gọi `client.connect` để thiết lập kết nối TCP đến broker.
    
2. **Xuất bản tin nhắn:** Hàm `publish` chạy một vòng lặp, mỗi giây gửi một tin nhắn đến chủ đề (topic) đã định nghĩa. Lệnh `client.publish(topic, msg)` là lệnh cốt lõi để gửi dữ liệu. Kết quả trả về cho biết tin nhắn đã được gửi thành công hay chưa.  
    
3. **Vòng lặp mạng:** `client.loop_start()` khởi chạy một luồng riêng để xử lý lưu lượng mạng (gửi/nhận tin nhắn, duy trì kết nối). Điều này rất quan trọng để ứng dụng chính không bị chặn. `client.loop_stop()` được gọi để đóng kết nối một cách an toàn.  
    

#### Phân Tích Sâu Mã Nguồn: Python OPC-UA Client

Dưới đây là ví dụ mã nguồn và phân tích một client OPC-UA tối giản sử dụng thư viện `opcua-asyncio` để đọc một biến từ server.  

Python

```
import asyncio
from asyncua import Client

url = "opc.tcp://localhost:4840/freeopcua/server/"
namespace = "http://examples.freeopcua.github.io"

async def main():
    print(f"Connecting to {url}...")
    async with Client(url=url) as client:
        # Tìm chỉ số namespace
        nsidx = await client.get_namespace_index(namespace)
        print(f"Namespace Index for '{namespace}': {nsidx}")

        # Lấy node của biến để đọc/ghi
        var = await client.nodes.root.get_child(
            f"0:Objects/{nsidx}:MyObject/{nsidx}:MyVariable"
        )
        value = await var.read_value()
        print(f"Value of MyVariable ({var}): {value}")

if __name__ == "__main__":
    asyncio.run(main())
```

**Phân tích mã nguồn:**

1. **Kết nối không đồng bộ:** Mã nguồn sử dụng `asyncio` và cú pháp `async with Client(...)` để quản lý kết nối một cách không đồng bộ. Điều này hiệu quả cho các ứng dụng công nghiệp cần xử lý nhiều tác vụ đồng thời.  
    
2. **Namespace và Node:** OPC-UA tổ chức dữ liệu trong các `namespace`. Hàm `get_namespace_index` được dùng để lấy chỉ số của namespace tùy chỉnh. Sau đó, `client.nodes.root.get_child` được sử dụng để duyệt cây địa chỉ của server và lấy đối tượng `Node` của biến cần đọc.  
    
3. **Đọc giá trị:** Phương thức `var.read_value()` thực hiện yêu cầu đến server để đọc giá trị hiện tại của biến. Thư viện tự động chuyển đổi kiểu dữ liệu OPC-UA sang kiểu dữ liệu tương ứng của Python.  
    

### 2.3 Theo Dõi Tồn Kho và Nguyên Vật Liệu Thời Gian Thực

#### Nền Tảng Mô Hình Dữ Liệu

Quản lý tồn kho chính xác là nền tảng của mọi hoạt động sản xuất hiệu quả. Để hiểu cách một hệ thống mạnh mẽ mô hình hóa dữ liệu này, chúng ta sẽ phân tích mã nguồn Python của DocType `Item` trong ERPNext (`item.py`).  

**Phân tích mã nguồn `Item.py`:** Mô hình dữ liệu của một mặt hàng (Item) trong ERPNext rất toàn diện, bao gồm các thuộc tính quan trọng cho cả hoạt động kho, sản xuất và kinh doanh.

- **Các trường cờ (boolean fields):** Các trường như `is_stock_item`, `has_batch_no`, `has_serial_no` xác định cách hệ thống sẽ xử lý mặt hàng. `is_stock_item` quyết định liệu các giao dịch kho có được ghi nhận hay không. `has_batch_no` và `has_serial_no` kích hoạt việc theo dõi theo lô hoặc số sê-ri, rất quan trọng cho việc truy xuất nguồn gốc và quản lý hạn sử dụng.  
    
- **Quản lý Tái đặt hàng:** Bảng con `reorder_levels` cho phép thiết lập các mức tồn kho tối thiểu cho từng kho. Khi tồn kho giảm xuống dưới mức này, hệ thống có thể tự động tạo yêu cầu vật tư, giúp tự động hóa quy trình bổ sung hàng.  
    
- **Định giá và Đơn vị tính:** Các trường `valuation_method` (FIFO, Moving Average) và `stock_uom` (đơn vị tồn kho cơ bản) là nền tảng cho việc tính toán giá trị tồn kho và quản lý số lượng. Bảng `uoms` định nghĩa các hệ số chuyển đổi giữa các đơn vị tính khác nhau (ví dụ: hộp, kg, cái).  
    
- **Các phương thức quan trọng:**
    
    - `set_opening_stock`: Tạo một bút toán nhập kho ban đầu (Stock Entry) khi một mặt hàng mới được tạo với số lượng tồn kho đầu kỳ.  
        
    - `validate_uom`: Đảm bảo tính nhất quán của đơn vị tính trong các giao dịch và ngăn chặn việc thay đổi đơn vị tính cơ bản sau khi đã có giao dịch phát sinh.  
        

#### Hiện Đại Hóa Việc Ghi Nhận Dữ Liệu: Quét Mã QR

Việc sử dụng mã QR (Quick Response) có thể cách mạng hóa các hoạt động kho bãi bằng cách tăng tốc độ và giảm thiểu sai sót trong các quy trình như nhận hàng, soạn hàng và kiểm kê. Thay vì nhập liệu thủ công, nhân viên kho chỉ cần dùng một thiết bị di động để quét mã, thông tin sẽ được ghi nhận ngay lập tức.

#### Phân Tích Sâu Mã Nguồn: Trình Quét Mã QR bằng JavaScript

Dưới đây là ví dụ và phân tích mã nguồn HTML và JavaScript để triển khai một trình quét mã QR trên nền tảng web sử dụng thư viện `html5-qrcode`.  

**Mã HTML:** Cấu trúc HTML rất tối giản, chỉ cần một vùng chứa cho trình quét và một vùng để hiển thị kết quả.

HTML

```
<html>
<head>
    <title>Html-Qrcode Demo</title>
</head>
<body>
    <div id="qr-reader" style="width:500px"></div>
    <div id="qr-reader-results"></div>

    <script src="https://unpkg.com/html5-qrcode"></script>
    <script src="scanner.js"></script>
</body>
</html>
```

**Mã JavaScript (`scanner.js`):** Đoạn mã này khởi tạo trình quét, định nghĩa các hàm callback và bắt đầu quá trình quét.

JavaScript

```
function onScanSuccess(decodedText, decodedResult) {
    // Xử lý kết quả quét thành công ở đây.
    console.log(`Scan result: ${decodedText}`, decodedResult);
    
    // Hiển thị kết quả trên trang
    let resultContainer = document.getElementById('qr-reader-results');
    resultContainer.innerHTML += `<div> - ${decodedText}</div>`;
    
    // Tùy chọn: Dừng quét sau khi tìm thấy kết quả
    // html5QrcodeScanner.clear();
}

function onScanError(errorMessage) {
    // Xử lý lỗi quét ở đây.
    // console.warn(`QR code scan error: ${errorMessage}`);
}

// Đảm bảo DOM đã sẵn sàng
document.addEventListener("DOMContentLoaded", (event) => {
    var html5QrcodeScanner = new Html5QrcodeScanner(
      "qr-reader", { fps: 10, qrbox: 250 });
    html5QrcodeScanner.render(onScanSuccess, onScanError);
});
```

**Phân tích mã nguồn:**

1. **Thiết lập HTML:** Hai thẻ `div` với ID `qr-reader` và `qr-reader-results` được tạo ra. Thẻ đầu tiên sẽ là nơi hiển thị giao diện camera của trình quét, và thẻ thứ hai dùng để xuất kết quả.  
    
2. **Khởi tạo Trình quét:** Trong JavaScript, một đối tượng `Html5QrcodeScanner` mới được tạo. Tham số đầu tiên, `"qr-reader"`, là ID của thẻ `div` nơi trình quét sẽ được hiển thị. Tham số thứ hai là một đối tượng cấu hình, cho phép tùy chỉnh các thông số như `fps` (khung hình mỗi giây) và `qrbox` (kích thước của hộp nhận diện QR code).  
    
3. **Hàm Callback `onScanSuccess`:** Đây là hàm quan trọng nhất. Nó sẽ được tự động gọi mỗi khi trình quét nhận diện và giải mã thành công một mã QR. Hàm này nhận `decodedText` (nội dung văn bản của mã QR) làm tham số. Bên trong hàm này, logic nghiệp vụ sẽ được thực thi, chẳng hạn như gửi `decodedText` đến máy chủ thông qua một lệnh gọi API.  
    
4. **Bắt đầu Quét:** Lệnh `html5QrcodeScanner.render(onScanSuccess, onScanError)` khởi động camera và bắt đầu quá trình quét liên tục.  
    

Sự kết hợp giữa một mô hình dữ liệu backend mạnh mẽ và một giao diện người dùng hiện đại, hiệu quả là yếu tố quyết định sự thành công của một hệ thống quản lý sản xuất số. Một mô hình dữ liệu vững chắc như của ERPNext đảm bảo tính toàn vẹn và chính xác của thông tin. Trong khi đó, một giao diện người dùng tối ưu hóa cho tầng sản xuất, như việc sử dụng trình quét mã QR, giúp giảm thiểu rào cản nhập liệu và đảm bảo dữ liệu được cập nhật theo thời gian thực. Giá trị thực sự được tạo ra khi có sự cộng sinh giữa hai yếu tố này: hành động vật lý (quét một linh kiện) được chuyển đổi ngay lập tức thành một bản ghi kỹ thuật số chính xác trong hệ thống.

### 2.4 Điều Khiển Chương Trình thông qua API REST

#### Tự Động Hóa Quy Trình Sản Xuất

API REST (Representational State Transfer) là phương tiện chính để tự động hóa và tích hợp các hệ thống phần mềm. Bằng cách sử dụng các API này, các ứng dụng tùy chỉnh, hệ thống của bên thứ ba, hoặc các kịch bản tự động có thể tương tác với hệ thống MES/ERP để tạo, đọc, cập nhật và xóa các tài liệu sản xuất cốt lõi như Lệnh Sản xuất (Manufacturing Order) và Lệnh Công việc (Work Order).

#### Phân Tích Sâu Mã Nguồn: Tạo Lệnh Sản Xuất trong Odoo

Việc tạo một Lệnh Sản xuất (`mrp.production`) trong Odoo thông qua API không đơn giản chỉ là gọi phương thức `create`. Một bước quan trọng và thường bị bỏ qua là phải mô phỏng sự kiện `onchange` để hệ thống tự động điền các thành phần nguyên vật liệu từ Định mức Nguyên vật liệu (Bill of Materials - BoM).  

Dưới đây là ví dụ mã nguồn Python minh họa quy trình này:

Python

```
# Giả sử 'models' là một đối tượng đã được xác thực để gọi API Odoo
# product_id là ID của sản phẩm cần sản xuất

# Bước 1: Mô phỏng onchange để lấy thông tin BoM
onchange_spec = models.execute_kw(db, uid, password,
    'mrp.production', 'onchange',
    [{'product_id': product_id}],
    {'onchange_fields': ['product_id']}
)
bom_details = onchange_spec['value']

# Bước 2: Chuẩn bị dữ liệu cho việc tạo Lệnh Sản xuất
# Dữ liệu này bao gồm các thành phần từ bom_details
production_values = {
    'product_id': product_id,
    'product_qty': 1,
    'product_uom_id': bom_details.get('product_uom_id'),
    'bom_id': bom_details.get('bom_id'),
    'move_raw_ids':,
    #... các trường cần thiết khác
}

# Tạo các dòng nguyên vật liệu (stock.move)
for move_raw in bom_details.get('move_raw_ids',):
    if move_raw == 0: # Lệnh 'create' cho one2many
        production_values['move_raw_ids'].append((0, 0, move_raw[1]))

# Bước 3: Tạo Lệnh Sản xuất
production_id = models.execute_kw(db, uid, password,
    'mrp.production', 'create',
    [production_values]
)

# Bước 4: Xác nhận và xử lý Lệnh Sản xuất
if production_id:
    # Xác nhận lệnh sản xuất
    models.execute_kw(db, uid, password, 'mrp.production', 'action_confirm', [[production_id]])
    
    # Đánh dấu là đã hoàn thành (ví dụ)
    models.execute_kw(db, uid, password, 'mrp.production', 'button_mark_done', [[production_id]])

print(f"Created Manufacturing Order with ID: {production_id}")
```

**Phân tích mã nguồn:**

1. **Mô phỏng `onchange`:** Lệnh gọi API đầu tiên không phải là `create` mà là `onchange`. Bằng cách này, chúng ta yêu cầu Odoo tính toán các giá trị mặc định và các dòng liên quan (như `move_raw_ids` cho nguyên vật liệu) như thể một người dùng vừa chọn sản phẩm trên giao diện.  
    
2. **Xây dựng Dữ liệu:** Dữ liệu trả về từ `onchange` được sử dụng để xây dựng đối tượng `production_values`. Đặc biệt, `move_raw_ids` được điền bằng cách sử dụng cú pháp đặc biệt của Odoo cho các trường quan hệ one2many: `(0, 0, {values})` để tạo một bản ghi mới.  
    
3. **Tạo và Xử lý:** Sau khi có đầy đủ dữ liệu, phương thức `create` được gọi. Các bước tiếp theo như `action_confirm` và `button_mark_done` được gọi để chuyển lệnh sản xuất qua các trạng thái khác nhau trong vòng đời của nó.  
    

#### Phân Tích Sâu Mã Nguồn: Tạo Lệnh Công Việc trong ERPNext

Trong ERPNext, quy trình tạo Lệnh Công việc (Work Order) từ một Đơn Bán hàng (Sales Order) được thực hiện thông qua một hàm đã được đưa vào danh sách trắng (whitelisted function) là `make_work_orders`. Thách thức chính đối với các nhà phát triển là xây dựng đúng cấu trúc của tham số  

`items` mà hàm này yêu cầu.

Dưới đây là một ví dụ tổng hợp về cách thực hiện lệnh gọi API này bằng Python, sử dụng thư viện `requests`:

Python

```
import requests
import json

# Thông tin xác thực và endpoint
erpnext_url = "https://your.erpnext.instance"
api_key = "your_api_key"
api_secret = "your_api_secret"
headers = {
    'Authorization': f"token {api_key}:{api_secret}",
    'Content-Type': 'application/json',
    'Accept': 'application/json'
}

# Tên của Đơn Bán hàng nguồn
sales_order_name = "SO-00001"

# Bước 1: Lấy thông tin chi tiết từ Đơn Bán hàng để xây dựng payload 'items'
# Đây là bước phức tạp, cần truy vấn các mặt hàng trong SO và BoM của chúng.
# Giả sử chúng ta đã có được cấu trúc 'items' cần thiết.
# Cấu trúc này thường bao gồm item_code, quantity, bom_no, v.v.
items_payload =

# Bước 2: Gọi hàm whitelisted 'make_work_orders'
api_endpoint = f"{erpnext_url}/api/method/erpnext.selling.doctype.sales_order.sales_order.make_work_orders"

data = {
    "source_name": sales_order_name,
    "items": json.dumps(items_payload) # 'items' thường được truyền dưới dạng chuỗi JSON
}

try:
    response = requests.post(api_endpoint, headers=headers, data=data)
    response.raise_for_status()  # Ném lỗi nếu có mã trạng thái HTTP lỗi

    # Phản hồi thành công thường chứa tên của các Work Order đã được tạo
    created_work_orders = response.json().get('message')
    print(f"Successfully created Work Orders: {created_work_orders}")

except requests.exceptions.HTTPError as err:
    print(f"HTTP Error: {err}")
    print(f"Response content: {err.response.text}")
except Exception as e:
    print(f"An error occurred: {e}")
```

**Phân tích mã nguồn:**

1. **Xác thực:** ERPNext sử dụng xác thực dựa trên token (API Key và Secret) được truyền trong header `Authorization`.  
    
2. **Endpoint:** Endpoint của API trỏ trực tiếp đến hàm Python được whitelisted trong backend của ERPNext: `erpnext.selling.doctype.sales_order.sales_order.make_work_orders`.  
    
3. **Payload Dữ liệu:** Dữ liệu được gửi dưới dạng `POST`. `source_name` là tên của Đơn Bán hàng gốc. Tham số `items` là phần phức tạp nhất; nó phải là một chuỗi JSON chứa một danh sách các đối tượng, mỗi đối tượng mô tả một mặt hàng cần tạo Lệnh Công việc. Việc xây dựng chính xác payload này đòi hỏi phải hiểu logic của hàm `get_work_order_items` trong mã nguồn của ERPNext, mặc dù hàm này không được whitelisted.  
    

## Phần 3: Trực Quan Hóa, Giám Sát và Triển Khai Chiến Lược

Phần cuối cùng này tập trung vào cách trực quan hóa dữ liệu sản xuất để thúc đẩy cải tiến và cung cấp một khuôn khổ chiến lược để lựa chọn và triển khai giải pháp phù hợp.

### 3.1 Xây Dựng Bảng Điều Khiển OEE Thời Gian Thực

#### Đo Lường Những Gì Quan Trọng: Hiệu Suất Thiết Bị Tổng Thể (OEE)

Hiệu suất Thiết bị Tổng thể (Overall Equipment Effectiveness - OEE) được coi là tiêu chuẩn vàng để đo lường năng suất sản xuất. Nó cung cấp một cái nhìn toàn diện về hiệu quả hoạt động bằng cách kết hợp ba yếu tố chính:

- **Tính sẵn sàng (Availability):** Tỷ lệ thời gian máy móc thực sự hoạt động so với thời gian dự kiến hoạt động. Mất mát do dừng máy không kế hoạch (hỏng hóc) và dừng máy có kế hoạch (chuyển đổi, bảo trì) được tính ở đây.  
    
- **Hiệu suất (Performance):** Tỷ lệ tốc độ sản xuất thực tế so với tốc độ thiết kế hoặc lý tưởng. Mất mát do chạy chậm và các điểm dừng nhỏ được tính ở đây.  
    
- **Chất lượng (Quality):** Tỷ lệ sản phẩm đạt chất lượng so với tổng số sản phẩm được sản xuất. Mất mát do sản phẩm lỗi và phải làm lại được tính ở đây.  
    

Công thức tính OEE là: OEE=Availability×Performance×Quality. Một điểm số OEE 100% đại diện cho một quy trình sản xuất hoàn hảo.  

#### Các Thành Phần Kiến Trúc của một Bảng Điều Khiển IoT

Một bảng điều khiển OEE thời gian thực hiệu quả đòi hỏi một kiến trúc nền tảng vững chắc để thu thập, xử lý và hiển thị dữ liệu. Các nền tảng IoT nguồn mở như ThingsBoard cung cấp một kiến trúc tham khảo tốt.  

- **Quản lý Thiết bị:** Khả năng đăng ký, cấu hình và giám sát trạng thái của các thiết bị và tài sản IoT.
    
- **Thu thập Dữ liệu:** Hỗ trợ nhiều giao thức (như MQTT, OPC-UA) để thu thập dữ liệu đo từ xa từ các cảm biến và máy móc.
    
- **Công cụ Quy tắc (Rule Engine):** Một thành phần mạnh mẽ cho phép xử lý dữ liệu đến theo thời gian thực. Các chuỗi quy tắc có thể được định nghĩa để chuyển đổi, chuẩn hóa dữ liệu, phát hiện các sự kiện bất thường, và kích hoạt cảnh báo.  
    
- **Trực quan hóa Dữ liệu:** Cung cấp các bảng điều khiển linh hoạt với một thư viện các widget (biểu đồ, đồng hồ đo, bản đồ) có thể tùy chỉnh để hiển thị dữ liệu một cách trực quan.  
    

#### Công Nghệ Frontend: React cho Bảng Điều Khiển

React đã trở thành một trong những thư viện JavaScript phổ biến nhất để xây dựng các giao diện người dùng hiện đại và tương tác. Sự phổ biến của nó trong việc phát triển bảng điều khiển được thể hiện qua số lượng lớn các mẫu bảng điều khiển quản trị (admin dashboard templates) nguồn mở có sẵn, cung cấp một nền tảng vững chắc để xây dựng các giao diện tùy chỉnh. Các mẫu này thường đi kèm với các thành phần giao diện người dùng (UI components) được xây dựng sẵn, biểu đồ, và các luồng xác thực cơ bản, giúp tăng tốc đáng kể quá trình phát triển.  

#### Phân Tích Mã Nguồn: Một Thành Phần Bảng Điều Khiển React Tiêu Biểu

Mặc dù không có mã nguồn cụ thể cho bảng điều khiển OEE, chúng ta có thể phân tích cấu trúc của một thành phần React tiêu biểu cho việc hiển thị dữ liệu thời gian thực, dựa trên các mẫu được tìm thấy.  

JavaScript

```
import React, { useState, useEffect } from 'react';
import { Line } from 'react-chartjs-2'; // Ví dụ sử dụng thư viện biểu đồ

// Component hiển thị chỉ số OEE
function OeeGauge({ label, value }) {
    // Logic để hiển thị một đồng hồ đo (gauge)
    return (
        <div className="oee-gauge">
            <h3>{label}</h3>
            <p>{(value * 100).toFixed(1)}%</p>
        </div>
    );
}

// Component chính của bảng điều khiển
function OeeDashboard() {
    const = useState({
        availability: 0,
        performance: 0,
        quality: 0,
        overall: 0
    });
    const = useState({ labels:, datasets: });

    // Sử dụng useEffect để fetch dữ liệu khi component được mount
    useEffect(() => {
        // Thiết lập kết nối WebSocket hoặc long-polling để nhận dữ liệu thời gian thực
        const fetchData = async () => {
            try {
                // Giả lập lệnh gọi API để lấy dữ liệu OEE
                const response = await fetch('/api/oee/realtime');
                const data = await response.json();
                
                const overallOee = data.availability * data.performance * data.quality;
                setOeeData({...data, overall: overallOee });

            } catch (error) {
                console.error("Failed to fetch OEE data:", error);
            }
        };

        // Fetch dữ liệu ban đầu và sau đó cập nhật mỗi 5 giây
        fetchData();
        const intervalId = setInterval(fetchData, 5000);

        // Hàm dọn dẹp để đóng kết nối khi component bị unmount
        return () => clearInterval(intervalId);
    },); // Mảng rỗng đảm bảo useEffect chỉ chạy một lần khi mount

    return (
        <div className="dashboard-container">
            <h1>OEE Dashboard</h1>
            <div className="gauges-container">
                <OeeGauge label="Availability" value={oeeData.availability} />
                <OeeGauge label="Performance" value={oeeData.performance} />
                <OeeGauge label="Quality" value={oeeData.quality} />
                <OeeGauge label="Overall OEE" value={ooeeData.overall} />
            </div>
            <div className="chart-container">
                {/* <Line data={historicalData} /> */}
            </div>
        </div>
    );
}

export default OeeDashboard;
```

**Phân tích mã nguồn:**

1. **Cấu trúc Component:** Component được viết dưới dạng hàm (functional component) sử dụng các hook của React như `useState` và `useEffect`.
    
2. **Quản lý Trạng thái:** `useState` được sử dụng để lưu trữ dữ liệu OEE hiện tại (`oeeData`) và dữ liệu lịch sử cho biểu đồ (`historicalData`).
    
3. **Lấy Dữ liệu:** `useEffect` được dùng để thực hiện các tác vụ phụ (side effects) như lấy dữ liệu từ API. Trong ví dụ này, một `setInterval` được sử dụng để mô phỏng việc cập nhật dữ liệu thời gian thực bằng cách gọi API mỗi 5 giây. Trong một ứng dụng thực tế, điều này có thể được thay thế bằng một kết nối WebSocket để có hiệu suất tốt hơn.
    
4. **Tích hợp Biểu đồ:** Component sử dụng một thư viện biểu đồ bên ngoài (ví dụ: `react-chartjs-2`) để trực quan hóa dữ liệu. Component `Line` sẽ nhận `historicalData` từ state để vẽ biểu đồ.
    

Sự chuyển dịch từ các báo cáo tĩnh cuối ngày sang các bảng điều khiển thời gian thực, có khả năng tương tác, là một sự thay đổi mô hình cơ bản trong quản lý sản xuất. Giá trị của một hệ thống MES hiện đại không chỉ nằm ở việc lưu trữ hồ sơ, mà còn ở việc cung cấp các vòng lặp phản hồi tức thì. Một bảng điều khiển OEE thời gian thực, được xây dựng bằng các công nghệ frontend hiện đại như React và được cung cấp dữ liệu từ các luồng IIoT, biến hệ thống từ một kho dữ liệu thụ động thành một công cụ tình báo hoạt động chủ động. Điều này cho phép giải quyết vấn đề một cách nhanh chóng ngay tại tầng sản xuất, một nguyên lý cốt lõi của Công nghiệp 4.0.

### 3.2 Một Khuôn Khổ để Lựa Chọn và Triển Khai

#### Tổng Hợp Phân Tích

Việc lựa chọn một nền tảng phần mềm sản xuất nguồn mở là một quyết định quan trọng với những tác động lâu dài. Dựa trên các phân tích trước đó, một khuôn khổ ra quyết định có hệ thống có thể được xây dựng.

#### Các Tiêu Chí Lựa Chọn Chính

Các tiêu chí sau đây, được mở rộng từ các khuyến nghị của chuyên gia , nên được xem xét cẩn thận:  

- **Phạm vi Chức năng:** Nền tảng có cung cấp các mô-đun MES/ERP cần thiết ngay từ đầu không? (ví dụ: quản lý BoM, lệnh sản xuất, theo dõi chất lượng).
    
- **Phù hợp với Ngăn xếp Công nghệ:** Nền tảng có phù hợp với chuyên môn kỹ thuật nội bộ không (Python, Java,.NET, TypeScript)? Việc lựa chọn một ngăn xếp công nghệ quen thuộc sẽ giảm đáng kể thời gian học hỏi và tăng tốc độ phát triển.
    
- **Triết lý Kiến trúc:** Tổ chức ưu tiên một bộ giải pháp "tất cả trong một" (như Odoo, ERPNext) hay một nền tảng API-first có khả năng mở rộng cao (như Carbon)? Quyết định này ảnh hưởng đến chiến lược phát triển và tích hợp trong tương lai.
    
- **Giấy phép và Mô hình Thương mại:** Giấy phép (AGPL, LGPL, MIT) có tương thích với mô hình kinh doanh không? Có một lộ trình hỗ trợ thương mại khả thi khi cần thiết không?.  
    
- **Sức khỏe Cộng đồng và Hệ sinh thái:** Dự án có hoạt động tích cực không? Có một cộng đồng mạnh mẽ để hỗ trợ và một hệ sinh thái các addon/plugin phong phú không?.  
    
- **Dễ dàng Triển khai:** Nền tảng có hỗ trợ các phương pháp triển khai hiện đại như Docker không? Điều này rất quan trọng để đảm bảo quá trình CI/CD và quản lý môi trường hiệu quả.  
    

#### Các Chiến Lược Triển Khai

- **Cách tiếp cận "Tất cả trong một" (All-in-One):** Triển khai một hệ thống toàn diện như ERPNext hoặc Odoo. Phương pháp này phù hợp nhất cho các tổ chức tìm kiếm một nguồn chân lý duy nhất (single source of truth) với độ phức tạp tích hợp tối thiểu.
    
- **Cách tiếp cận "Phân lớp Mô-đun" (Modular Layering):** Kết hợp các công cụ tốt nhất trong từng lĩnh vực, như được các chuyên gia khuyến nghị. Một ví dụ về kiến trúc như vậy có thể bao gồm:  
    
    - **Lõi ERP/MES:** Sử dụng Odoo hoặc ERPNext để quản lý dữ liệu chủ, tồn kho và đơn hàng.
        
    - **Công cụ Lập lịch:** Tích hợp `frePPLe` để lập kế hoạch sản xuất nâng cao.
        
    - **Thu thập & Giám sát Dữ liệu:** Xây dựng một cổng IIoT tùy chỉnh bằng Python (sử dụng MQTT/OPC-UA) để đẩy dữ liệu vào một nền tảng như ThingsBoard hoặc một ngăn xếp tùy chỉnh gồm Grafana/InfluxDB.  
        
        Cách tiếp cận này mang lại sự linh hoạt tối đa nhưng đòi hỏi nỗ lực tích hợp đáng kể và một đội ngũ kỹ thuật có năng lực.
        

### 3.3 Kết Luận và Triển Vọng Tương Lai

#### Tóm Tắt các Phát Hiện Chính

Báo cáo này đã phân tích sâu về bối cảnh phần mềm quản lý sản xuất nguồn mở, từ các triết lý kiến trúc khác nhau đến các ví dụ triển khai mã nguồn cụ thể. Các xu hướng chính được xác định bao gồm sự tồn tại song song của các hệ thống ERP nguyên khối, toàn diện và các nền tảng MES API-first, hiện đại; tầm quan trọng của các công cụ lập lịch chuyên dụng; và vai trò không thể thiếu của các giao thức IIoT và các bảng điều khiển thời gian thực trong việc hiện thực hóa nhà máy số.

#### Khuyến Nghị Cuối Cùng

Dựa trên các phân tích, các khuyến nghị sau đây được đưa ra cho các hồ sơ người dùng giả định khác nhau:

- **Đối với Doanh nghiệp Vừa và Nhỏ (SME) có nguồn lực CNTT hạn chế:** Một giải pháp "tất cả trong một" như Odoo (Phiên bản Cộng đồng) hoặc qcadoo MES cung cấp một rào cản gia nhập thấp hơn, với các chức năng cốt lõi được tích hợp sẵn và một cộng đồng hỗ trợ mạnh mẽ.
    
- **Đối với Doanh nghiệp Lớn có đội ngũ phát triển lành nghề:** Một nền tảng API-first như Carbon hoặc một cách tiếp cận phân lớp mô-đun kết hợp ERPNext với các công cụ chuyên dụng sẽ cung cấp sự linh hoạt cần thiết để đáp ứng các yêu cầu phức tạp và tùy chỉnh cao.
    
- **Đối với Startup Công nghệ:** Một ngăn xếp công nghệ hiện đại như của Carbon (dựa trên TypeScript) có thể hấp dẫn hơn và phù hợp hơn với tài năng kỹ thuật hiện có, cho phép phát triển nhanh và tích hợp dễ dàng với các dịch vụ đám mây khác.
    

#### Xu Hướng Tương Lai

Tương lai của phần mềm sản xuất nguồn mở sẽ tiếp tục phát triển theo hướng thông minh hơn và kết nối hơn. Các xu hướng đáng chú ý bao gồm:

- **Tích hợp sâu hơn Trí tuệ Nhân tạo (AI) và Học máy (ML):** Sử dụng AI/ML cho bảo trì dự đoán, tối ưu hóa lịch trình động và kiểm soát chất lượng tự động.
    
- **Sự trỗi dậy của các Nền tảng Low-Code:** Các nền tảng như Frappe Framework cho phép người dùng không chuyên về kỹ thuật có thể tùy chỉnh các quy trình và báo cáo, dân chủ hóa việc phát triển ứng dụng.
    
- **Triển khai Cloud-Native:** Tầm quan trọng ngày càng tăng của việc đóng gói bằng container (Docker) và điều phối (Kubernetes) để triển khai các hệ thống sản xuất linh hoạt, có khả năng mở rộng và phục hồi cao trên nền tảng đám mây.
    

Nguồn được dùng trong báo cáo

[

![](https://t3.gstatic.com/faviconV2?url=https://www.viettelsoftware.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

viettelsoftware.com

DOANH NGHIỆP SẢN XUẤT NÊN CHỌN MES HAY ERP? - Viettel Software

Mở trong cửa sổ mới](https://www.viettelsoftware.com/doanh-nghiep-san-xuat-nen-chon-mes-hay-erp.html)[

![](https://t1.gstatic.com/faviconV2?url=https://macsphere.mcmaster.ca/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

macsphere.mcmaster.ca

AN OPEN-SOURCE MANUFACTURING EXECUTION SYSTEM - MacSphere

Mở trong cửa sổ mới](https://macsphere.mcmaster.ca/handle/11375/29871)[

![](https://t1.gstatic.com/faviconV2?url=https://mdcplus.fi/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

mdcplus.fi

Top Free & Open-Source MES Software for 2025 - MDCplus

Mở trong cửa sổ mới](https://mdcplus.fi/blog/top-free-mes-systems-manufacturing-execution/)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

crbnos/carbon: The open-source manufacturing ERP/MES ... - GitHub

Mở trong cửa sổ mới](https://github.com/crbnos/carbon)[

![](https://t1.gstatic.com/faviconV2?url=https://tulip.co/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

tulip.co

Open Source For Manufacturing: Key Lessons Manufacturers Can Learn - Tulip Interfaces

Mở trong cửa sổ mới](https://tulip.co/blog/open-source-for-manufacturing-key-lessons-manufacturers-can-learn/)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

frappe/erpnext: Free and Open Source Enterprise ... - GitHub

Mở trong cửa sổ mới](https://github.com/frappe/erpnext)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

Odoo. Open Source Apps To Grow Your Business. - GitHub

Mở trong cửa sổ mới](https://github.com/odoo/odoo)[

![](https://t0.gstatic.com/faviconV2?url=https://medium.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

medium.com

Top 10 Most-Starred Open-Source ERP and CRM on GitHub | by NocoBase - Medium

Mở trong cửa sổ mới](https://medium.com/@nocobase/top-10-most-starred-open-source-erp-and-crm-on-github-9a3d585eeb9e)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

iplus-framework/iPlusMES: Manufacturing Execution System based on iplus-framework

Mở trong cửa sổ mới](https://github.com/iplus-framework/iPlusMES)[

![](https://t0.gstatic.com/faviconV2?url=https://docs.erpnext.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

docs.erpnext.com

ERPNext Documentation

Mở trong cửa sổ mới](https://docs.erpnext.com/)[

![](https://t1.gstatic.com/faviconV2?url=https://codewithkarani.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

codewithkarani.com

Creating and Managing Items in ERPNext - Code with Karani

Mở trong cửa sổ mới](https://codewithkarani.com/2025/01/19/creating-and-managing-items-in-erpnext/)[

![](https://t0.gstatic.com/faviconV2?url=https://medevel.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

medevel.com

10+ Open-source and Free Manufacturing ERP and Manufacturing Management Solutions

Mở trong cửa sổ mới](https://medevel.com/os-erp-and-manufacturing-solutions/)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

erp · GitHub Topics

Mở trong cửa sổ mới](https://github.com/topics/erp)[

![](https://t2.gstatic.com/faviconV2?url=https://opensource.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

opensource.com

Top 9 open source ERP systems to consider | Opensource.com

Mở trong cửa sổ mới](https://opensource.com/tools/enterprise-resource-planning)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

Odoo Industry Apps - GitHub

Mở trong cửa sổ mới](https://github.com/odoo/industry)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

OCA/manufacture: Odoo Manufacturing Addons - GitHub

Mở trong cửa sổ mới](https://github.com/OCA/manufacture)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

qcadoo MES - friendly web manufacturing software - GitHub

Mở trong cửa sổ mới](https://github.com/qcadoo/mes)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

sindohmes/mes4u: MES Open Source System - GitHub

Mở trong cửa sổ mới](https://github.com/sindohmes/mes4u)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

dothinking/jsp_framework: A Python library for implementing and testing algorithm for Job-Shop Scheduling problem. - GitHub

Mở trong cửa sổ mới](https://github.com/dothinking/jsp_framework)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

taghubnet/frePPLe - open source production planning - GitHub

Mở trong cửa sổ mới](https://github.com/taghubnet/frePPLe)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

jobshop-scheduling · GitHub Topics

Mở trong cửa sổ mới](https://github.com/topics/jobshop-scheduling)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

bharatpurohit97/Job-Shop-Scheduling-GeneticAlgorithm - GitHub

Mở trong cửa sổ mới](https://github.com/bharatpurohit97/Job-Shop-Scheduling-GeneticAlgorithm)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

job-shop-scheduling-problem · GitHub Topics

Mở trong cửa sổ mới](https://github.com/topics/job-shop-scheduling-problem)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

scheduling-algorithms · GitHub Topics

Mở trong cửa sổ mới](https://github.com/topics/scheduling-algorithms?l=python&o=desc&s=updated)[

![](https://t0.gstatic.com/faviconV2?url=https://wurmen.github.io/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

wurmen.github.io

Example1

Mở trong cửa sổ mới](https://wurmen.github.io/Genetic-Algorithm-for-Job-Shop-Scheduling-and-NSGA-II/implementation%20with%20python/GA-jobshop/Example1.html)[

![](https://t1.gstatic.com/faviconV2?url=https://www.emqx.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

emqx.com

MQTT in Python with Paho Client: Beginner's Guide 2025 | EMQ

Mở trong cửa sổ mới](https://www.emqx.com/en/blog/how-to-use-mqtt-in-python)[

![](https://t3.gstatic.com/faviconV2?url=https://opcua-asyncio.readthedocs.io/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

opcua-asyncio.readthedocs.io

Python opcua-asyncio Documentation — opcua-asyncio documentation - Read the Docs

Mở trong cửa sổ mới](https://opcua-asyncio.readthedocs.io/)[

![](https://t3.gstatic.com/faviconV2?url=https://opcua-asyncio.readthedocs.io/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

opcua-asyncio.readthedocs.io

A Minimal OPC-UA Client — opcua-asyncio documentation

Mở trong cửa sổ mới](https://opcua-asyncio.readthedocs.io/en/latest/usage/get-started/minimal-client.html)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

erpnext/erpnext/stock/doctype/item/item.py at develop · frappe ...

Mở trong cửa sổ mới](https://github.com/frappe/erpnext/blob/develop/erpnext/stock/doctype/item/item.py)[

![](https://t2.gstatic.com/faviconV2?url=https://frappe.io/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

frappe.io

Open Source ERP Software for Inventory Management - Frappe

Mở trong cửa sổ mới](https://frappe.io/erpnext/open-source-inventory-management-system)[

![](https://t1.gstatic.com/faviconV2?url=https://codewithkarani.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

codewithkarani.com

Getting Started with ERPNext Inventory Management - Code with Karani

Mở trong cửa sổ mới](https://codewithkarani.com/2025/01/18/getting-started-with-erpnext-inventory-management/)[

![](https://t0.gstatic.com/faviconV2?url=https://gist.github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

gist.github.com

Demo code on using github.com/mebjas/html5-qrcode. This was ...

Mở trong cửa sổ mới](https://gist.github.com/mebjas/729c5397506a879ec704075c8a5284e8)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

React example using html5-qrcode library - GitHub

Mở trong cửa sổ mới](https://github.com/scanapp-org/html5-qrcode-react)[

![](https://t0.gstatic.com/faviconV2?url=https://www.odoo.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

odoo.com

How to create manufacturing order using API? | Odoo

Mở trong cửa sổ mới](https://www.odoo.com/forum/help-1/how-to-create-manufacturing-order-using-api-182874)[

![](https://t0.gstatic.com/faviconV2?url=https://stackoverflow.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

stackoverflow.com

How do I consume and produce a manufacturing order in Odoo using xml-rpc?

Mở trong cửa sổ mới](https://stackoverflow.com/questions/40382710/how-do-i-consume-and-produce-a-manufacturing-order-in-odoo-using-xml-rpc)[

![](https://t3.gstatic.com/faviconV2?url=https://discuss.frappe.io/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

discuss.frappe.io

Create work orders from sales order with API - Manufacturing ...

Mở trong cửa sổ mới](https://discuss.frappe.io/t/create-work-orders-from-sales-order-with-api/67153)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

alyf-de/frappe_api-docs: Unofficial documentation of the Frappe / ERPNext API - GitHub

Mở trong cửa sổ mới](https://github.com/alyf-de/frappe_api-docs)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

point85/OEE-Designer: The OEE-Designer is the build time ... - GitHub

Mở trong cửa sổ mới](https://github.com/point85/OEE-Designer)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

ManufacturingCSU/OEE: Assets to build operational visibility solutions using Microsoft Manufacturing Cloud - GitHub

Mở trong cửa sổ mới](https://github.com/ManufacturingCSU/OEE)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

thingsboard/thingsboard: Open-source IoT Platform ... - GitHub

Mở trong cửa sổ mới](https://github.com/thingsboard/thingsboard)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

React Dashboards - Open-Source and Free | Admin-Dashboards.com - GitHub

Mở trong cửa sổ mới](https://github.com/admin-dashboards/react-dashboards)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

react-dashboards · GitHub Topics

Mở trong cửa sổ mới](https://github.com/topics/react-dashboards)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

react-dashboard · GitHub Topics

Mở trong cửa sổ mới](https://github.com/topics/react-dashboard)[

![](https://t3.gstatic.com/faviconV2?url=https://akpolatcem.medium.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

akpolatcem.medium.com

Designing IoT Middleware Dashboard with React using AI/Claude | by ca - Medium

Mở trong cửa sổ mới](https://akpolatcem.medium.com/designing-iot-middleware-dashboard-using-ai-claude-b4a40aa1c518)[

![](https://t1.gstatic.com/faviconV2?url=https://github.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

github.com

metasfresh/metasfresh: We do Open Source ERP - Fast, Flexible & Free Software to scale your Business. - GitHub





](https://github.com/metasfresh/metasfresh)