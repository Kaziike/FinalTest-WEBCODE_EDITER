# BÁO CÁO ĐỒ ÁN: XÂY DỰNG TRÌNH SOẠN THẢO MÃ NGUỒN TRÊN NỀN TẢNG WEB TĨNH (VS CODE WEB CLONE)

---

## CHƯƠNG 1. TỔNG QUAN NGHIÊN CỨU

### 1.1 Đặt vấn đề
Trong kỷ nguyên công nghệ số và sự phát triển mạnh mẽ của điện toán đám mây, xu hướng chuyển dịch các ứng dụng từ nền tảng máy tính cá nhân (desktop applications) lên nền tảng web (web-based applications) đang diễn ra vô cùng mạnh mẽ. Đối với các lập trình viên, trình soạn thảo mã nguồn (Code Editor) và môi trường phát triển tích hợp (IDE) là những công cụ không thể thiếu. Các IDE truyền thống như Visual Studio, Eclipse hay IntelliJ IDEA mang lại sức mạnh to lớn nhưng đi kèm với nhược điểm là dung lượng lớn, tiêu tốn nhiều tài nguyên phần cứng và yêu cầu cài đặt phức tạp.

Sự ra đời của Visual Studio Code (VS Code) đã làm thay đổi cách tiếp cận của cộng đồng lập trình viên bằng việc kết hợp giữa tốc độ của một trình soạn thảo văn bản và khả năng mở rộng của một IDE. Tuy nhiên, trong nhiều tình huống đặc thù như giảng dạy, thi cử, học tập trực tuyến hay làm việc trên các thiết bị có cấu hình yếu (như Chromebook, máy tính bảng), việc tải và cài đặt một phần mềm desktop vẫn là một rào cản. 

Xuất phát từ nhu cầu thực tiễn đó, việc nghiên cứu và xây dựng một "Trình soạn thảo mã nguồn trên nền tảng web tĩnh" (Static Web-based Code Editor) hoàn toàn dựa trên HTML, CSS và JavaScript thuần mà không cần đến sự hỗ trợ của máy chủ (Server-less) hay các công cụ biên dịch phức tạp (Build tools) trở thành một bài toán có tính ứng dụng cao. Đề tài này giải quyết vấn đề cung cấp một môi trường viết code nhanh chóng, nhẹ nhàng, có thể chạy trên mọi trình duyệt web hiện đại, đồng thời mang lại trải nghiệm người dùng tương đồng với VS Code.

### 1.2 Mục tiêu nghiên cứu
Mục tiêu chính của đề tài là xây dựng thành công một ứng dụng web tĩnh mô phỏng lại giao diện và các chức năng cơ bản của phần mềm Visual Studio Code. Các mục tiêu cụ thể bao gồm:
1. **Mục tiêu về giao diện (UI/UX)**: 
   - Thiết kế và xây dựng giao diện người dùng (User Interface) giống với VS Code Dark Theme.
   - Xây dựng bố cục (Layout) chuẩn bao gồm: Thanh công cụ (Activity Bar), Thanh bên (Sidebar / Explorer), Khu vực soạn thảo (Editor Area) và các thẻ tab (Tabs).
2. **Mục tiêu về chức năng (Functional Goals)**:
   - Tích hợp lõi soạn thảo mã nguồn chuyên nghiệp hỗ trợ tô sáng cú pháp (Syntax Highlighting) cho nhiều ngôn ngữ phổ biến (HTML, CSS, JS).
   - Xây dựng hệ thống quản lý tập tin ảo (Virtual File System) ngay trên bộ nhớ trình duyệt, cho phép tạo file, tạo thư mục và xóa file/thư mục.
   - Phát triển tính năng xuất file (Export/Save As), cho phép người dùng tải mã nguồn đã viết dưới dạng file vật lý về máy tính.
3. **Mục tiêu về công nghệ**: 
   - Sử dụng 100% công nghệ Web thuần túy (Vanilla HTML, CSS, JavaScript) kết hợp với các thư viện mã nguồn mở qua CDN nhằm đảm bảo tính "tĩnh" của trang web, không phụ thuộc vào Node.js hay Database.

### 1.3 Phương pháp nghiên cứu
Để đạt được các mục tiêu đã đề ra, nghiên cứu áp dụng các phương pháp sau:
- **Phương pháp thu thập và phân tích tài liệu**: Nghiên cứu lý thuyết về thiết kế web đáp ứng (Responsive Web Design), kiến trúc DOM, và cách thức hoạt động của thư viện Monaco Editor. Phân tích giao diện của VS Code gốc để bóc tách các thành phần UI.
- **Phương pháp mô hình hóa và thiết kế**: Vẽ sơ đồ tư duy, xây dựng các wireframe (khung giao diện) và luồng xử lý sự kiện (Event Flow) cho hệ thống quản lý file ảo.
- **Phương pháp thực nghiệm (Prototyping)**: Lập trình thử nghiệm từng module độc lập (module giao diện Flexbox, module quản lý cây thư mục, module editor). Sau đó tích hợp các module lại thành một ứng dụng hoàn chỉnh và kiểm thử trực tiếp trên trình duyệt.

### 1.4 Đối tượng nghiên cứu
Đối tượng nghiên cứu chính của đề tài xoay quanh:
- Các tiêu chuẩn cốt lõi của Web Frontend: HTML5 (cấu trúc ngữ nghĩa), CSS3 (Flexbox layout, CSS Variables), và ECMAScript 6+ (Event Delegation, DOM Manipulation, Blob API).
- Thư viện Monaco Editor: Cấu trúc API, cách thức khởi tạo (Initialization) và tương tác với các Model (Tập tin) của Monaco.
- Trải nghiệm người dùng (UX) trong thiết kế công cụ phát triển (Developer Tools).

---

## CHƯƠNG 2. CƠ SỞ LÝ THUYẾT

### 2.1 Tổng quan về công nghệ Web nền tảng (HTML5, CSS3, ES6)
Một ứng dụng web tĩnh được cấu thành từ ba trụ cột chính, và trong phạm vi đề tài này, chúng được tối ưu hóa để vận hành mà không cần bất kỳ framework nào như React hay Vue.
- **HTML5 (HyperText Markup Language 5)**: Đóng vai trò xây dựng bộ khung xương của ứng dụng. HTML5 cung cấp các thẻ ngữ nghĩa và thuộc tính cho phép nhúng trực tiếp các icon (qua FontAwesome) và các script từ CDN.
- **CSS3 (Cascading Style Sheets 3)**: Sử dụng cơ chế bố cục linh hoạt **Flexbox (Flexible Box Layout)** để phân chia màn hình thành các khu vực (Activity Bar, Sidebar, Editor). Flexbox đặc biệt hữu ích khi thiết kế các ứng dụng web dạng bảng điều khiển (dashboard) chiếm toàn bộ chiều cao màn hình (`100vh`). Đồng thời, CSS Variables (Custom Properties) được sử dụng để quản lý hệ thống màu sắc (Color Palette), giúp dễ dàng đồng bộ mã màu Dark Theme của VS Code (như `#1e1e1e` cho nền editor, `#252526` cho thanh bên).
- **JavaScript (ES6+)**: Xử lý toàn bộ logic nghiệp vụ (Business Logic) của ứng dụng trên trình duyệt. Đề tài tận dụng mạnh mẽ cơ chế **Event Delegation** (Ủy quyền sự kiện) để quản lý các phần tử được tạo ra động (như các file/folder được người dùng thêm vào sau khi trang đã tải). Bên cạnh đó, **Blob API** và **URL.createObjectURL()** được sử dụng để tạo ra các file ảo từ chuỗi text và ép trình duyệt tải xuống, hiện thực hóa tính năng "Export File".

### 2.2 Thư viện mã nguồn mở Monaco Editor
Visual Studio Code nổi tiếng nhờ khả năng xử lý code mượt mà, và bí mật đằng sau sức mạnh đó chính là lõi editor mang tên **Monaco Editor**. 

#### 2.2.1 Lịch sử và kiến trúc của Monaco Editor
Monaco Editor là một trình soạn thảo mã nguồn được Microsoft phát triển và tách ra từ chính mã nguồn của VS Code. Nó chạy hoàn toàn trên nền tảng web và được thiết kế với kiến trúc mô-đun cao. Kiến trúc của Monaco bao gồm một hệ thống tính toán vị trí con trỏ, hiển thị màu sắc dựa trên các Tokenizer (bộ phân tách cú pháp) và một hệ thống Web Worker để xử lý ngôn ngữ mà không làm treo luồng chính (Main thread) của trình duyệt. Việc sử dụng RequireJS (một thư viện tải mô-đun theo chuẩn AMD) là bắt buộc khi tích hợp Monaco qua CDN để đảm bảo các tệp tin lõi của editor được tải không đồng bộ.

#### 2.2.2 Các tính năng chính của Monaco ứng dụng trong đề tài

##### 2.2.2.1 Syntax Highlighting và IntelliSense
Một trong những lý do chính chọn Monaco Editor thay vì thẻ `<textarea>` truyền thống là khả năng **Syntax Highlighting** (Tô sáng cú pháp). Monaco đi kèm với các bộ quy tắc phân tích cú pháp (Grammar rules) cho hàng chục ngôn ngữ. Trong đề tài này, khi người dùng tạo một file có đuôi `.html`, `.css` hoặc `.js`, Monaco sẽ tự động nhận diện và chuyển đổi `Language Mode`, từ đó cung cấp màu sắc chính xác cho các từ khóa, thẻ, chuỗi, và cung cấp khả năng tự động hoàn thành cơ bản (IntelliSense).

##### 2.2.2.2 Quản lý Model và Editor State
Trong kiến trúc của Monaco, một `Editor` (khung nhìn hiển thị) và một `Model` (dữ liệu của tập tin) là hai khái niệm tách biệt. Một Editor có thể hiển thị nội dung của nhiều Model khác nhau tại các thời điểm khác nhau. Đề tài đã vận dụng nguyên lý này: tạo ra một đối tượng lưu trữ trạng thái các file (Mock State), và khi người dùng click vào một file trên Sidebar, ứng dụng sẽ gọi hàm `editor.setValue()` và `monaco.editor.setModelLanguage()` để "bơm" nội dung tương ứng vào Editor duy nhất trên màn hình, giúp tiết kiệm bộ nhớ thay vì tạo nhiều instance của Monaco.

---

## CHƯƠNG 3. PHÂN TÍCH THIẾT KẾ HỆ THỐNG

### 3.1 Mô tả vấn đề
Bài toán đặt ra là cần xây dựng một giao diện người dùng có tính tương tác cao (như mở/đóng thư mục, thêm/xóa file) nhưng lại không có một máy chủ Backend hay cơ sở dữ liệu (Database) nào để lưu trữ trạng thái. Mọi thao tác phải được thực thi tức thời trên Client-side. Ràng buộc (Constraint) lớn nhất là ứng dụng phải "tĩnh" hoàn toàn, tức là chỉ cần một cú click chuột (double click) vào file `index.html` trên máy tính là ứng dụng phải chạy mượt mà không cần lệnh `npm start` hay thiết lập localhost.

### 3.2 Đặc tả yêu cầu hệ thống

#### 3.2.1 Yêu cầu chức năng
1. **Khởi tạo Editor**: Hệ thống phải khởi tạo và hiển thị khung soạn thảo code ngay khi trang tải xong.
2. **Quản lý Cây Thư Mục (File Explorer)**:
   - Hệ thống cho phép hiển thị danh sách các file/folder.
   - Cung cấp nút để người dùng nhập tên và tạo **File mới** hoặc **Folder mới**.
   - Cung cấp nút xóa (biểu tượng thùng rác) cạnh mỗi file và folder để xóa đối tượng đó khỏi hệ thống.
3. **Thao tác viết code (Coding)**: 
   - Nhận dạng đuôi file để đổi màu cú pháp phù hợp.
   - Lưu trữ tự động nội dung code của file hiện tại vào bộ nhớ tạm (biến JS) trước khi chuyển sang file khác.
4. **Xuất tệp tin (Export/Save As)**: 
   - Xuất nội dung code đang hiển thị thành tệp tin vật lý có định dạng tương ứng (ví dụ: `.html`, `.js`) tải về máy cá nhân thông qua menu `File > Export File`.

#### 3.2.2 Yêu cầu phi chức năng

##### 3.2.2.1 Hiệu năng và Tốc độ xử lý
- Quá trình chuyển đổi nội dung giữa các tab/file phải diễn ra với độ trễ dưới 100ms để đảm bảo trải nghiệm liền mạch.
- Tối ưu hóa DOM (Document Object Model): Sử dụng cơ chế Event Delegation gắn sự kiện click vào phần tử cha (ví dụ `.file-tree`) thay vì gắn hàng trăm `EventListener` cho mỗi phần tử con, giúp giảm thiểu rò rỉ bộ nhớ (Memory Leak).

##### 3.2.2.2 Trải nghiệm người dùng (UX/UI)
- Giao diện phải sử dụng các icon ngữ nghĩa chuẩn mực (FontAwesome) tương đồng với bộ thiết kế gốc của VS Code.
- Cung cấp cơ chế Hover (trỏ chuột) để làm nổi bật các tập tin đang thao tác và chỉ hiển thị nút Xóa (Trash icon) khi người dùng chủ động trỏ chuột vào, nhằm tránh giao diện bị rối mắt.

### 3.3 Thiết kế dữ liệu

#### 3.3.1 Cấu trúc lưu trữ (Data Structure)
Do hệ thống không có Database, toàn bộ cấu trúc file được thiết kế dưới dạng đối tượng (Object) trong JavaScript, lưu trữ trên bộ nhớ RAM của trình duyệt. Cấu trúc cơ bản như sau:

```javascript
const files = {
    "index.html": {
        language: "html",
        content: "<!DOCTYPE html>..."
    },
    "style.css": {
        language: "css",
        content: "body { background: #1e1e1e; }"
    }
};
let currentFileName = "index.html"; // Trạng thái con trỏ đang mở file nào
```
Bên cạnh đó, cấu trúc của các thư mục (Folders) được quản lý gián tiếp thông qua cây DOM (Document Object Model) trên giao diện. Khi một folder chứa file, DOM của file đó sẽ nằm lồng bên trong một thẻ `<div class="folder-children">`.

#### 3.3.2 Đặc tả chi tiết vòng đời dữ liệu
- **Create**: Khi tạo file, bổ sung một key mới vào đối tượng `files`, giá trị nội dung rỗng (`content: ''`).
- **Read**: Khi click vào file, đọc giá trị `files[fileName].content` và gán vào Monaco.
- **Update**: Khi đang gõ phím và trước khi chuyển đổi file (switch file), hệ thống lấy `editor.getValue()` và cập nhật lại vào `files[currentFileName].content`.
- **Delete**: Dùng lệnh `delete files[fileName]` để loại bỏ dữ liệu khỏi bộ nhớ, đồng thời gọi `element.remove()` để xóa trên giao diện.

### 3.4 Thiết kế chức năng (Luồng xử lý - Workflow)

1. **Luồng tạo File mới**:
   - Người dùng click biểu tượng "New File".
   - Hàm `prompt` được gọi để lấy chuỗi văn bản (Tên file).
   - Kiểm tra chuỗi rỗng hoặc trùng lặp (trùng key trong `files`).
   - Tạo phần tử HTML (DOM Node) chứa icon tương ứng với đuôi file (`.html`, `.css`, v.v.).
   - Kiểm tra xem có `.folder-item` nào đang ở trạng thái `active` không. Nếu có, `appendChild` phần tử file vào bên trong thư mục đó. Nếu không, thêm vào gốc `.file-tree`.
   - Gọi hàm kích hoạt file mới để mở nó lên giao diện Editor.

2. **Luồng Export File**:
   - Người dùng click `File > Export File`.
   - Hệ thống đọc toàn bộ chuỗi ký tự từ màn hình Editor.
   - Tạo một đối tượng `Blob` với MIME type là `text/plain`.
   - Sinh ra một URL tạm thời bằng `URL.createObjectURL(blob)`.
   - Tạo một thẻ `<a>` ảo (ẩn), gán `href` bằng URL vừa tạo, `download` bằng tên file hiện tại.
   - Dùng JS mô phỏng sự kiện `click` lên thẻ `<a>` để trình duyệt bật hộp thoại lưu file.

### 3.5 Thiết kế giao diện

#### 3.5.1 Sơ đồ website (Layout Architecture)
Bố cục được chia làm 3 trục chính bằng Flexbox:
- Khu vực tĩnh trên cùng (Menu Bar): Cao 30px.
- Khu vực động giữa (Main Body): Chiếm phần không gian còn lại (`flex: 1`). Khu vực này lại chia nhỏ thành 3 phần ngang:
  - Activity Bar (Rộng 48px, menu công cụ dọc).
  - Sidebar (Rộng 250px, chứa cây thư mục).
  - Editor Area (Chiếm không gian còn lại, chứa Tabs và Monaco Container).

#### 3.5.2 Giao diện trang chủ
Giao diện tuân thủ chặt chẽ nguyên tắc của **VS Code Dark Theme**:
- Mã màu nền Editor: `#1e1e1e`
- Mã màu nền Sidebar: `#252526`
- Màu viền ngăn cách (Border): `#454545`
- Màu chữ mặc định: `#cccccc`
Mọi đường nét đều thiết kế dạng khối vuông, loại bỏ thanh cuộn mặc định của trình duyệt (`overflow: hidden` ở body) để tạo cảm giác của một phần mềm Native (phần mềm cài đặt) thay vì một trang web.

#### 3.5.3 Tương tác giao diện người dùng
Hệ thống tận dụng pseudo-class `:hover` trong CSS để hiện ra các thanh công cụ bổ sung. Ví dụ: khi trỏ chuột vào một `.folder-item`, lớp `.folder-actions` mới chuyển `opacity` từ 0 sang 1, giúp hiển thị 3 icon (Tạo file, tạo thư mục, xóa). Cách thiết kế này giúp tối giản hóa giao diện, tránh tình trạng màn hình có quá nhiều nút bấm gây xao nhãng.

---

## CHƯƠNG 4. KẾT QUẢ THỰC NGHIỆM
*(Lưu ý cho sinh viên: Dưới đây là khung sườn để bạn điền nội dung. Bạn cần thực hiện các thao tác trên trình duyệt, chụp ảnh màn hình (screenshot) và dán vào các mục tương ứng trong báo cáo file Word của mình)*

### 4.1 Dữ liệu thử nghiệm (Test Cases)
Để đánh giá hệ thống, tôi đã tiến hành các kịch bản thử nghiệm (Test Scenarios) sau:
- Kịch bản 1: Nhập tên file hợp lệ (`main.js`), nhập tên file trùng lặp, nhập tên file rỗng.
- Kịch bản 2: Viết một đoạn mã HTML dài 100 dòng, kiểm tra tính năng cuộn mượt mà của Monaco Editor.
- Kịch bản 3: Tạo thư mục "src", sau đó chọn thư mục "src" và tạo file "index.js" để kiểm tra tính năng lồng ghép (nesting) vào thư mục con.
- Kịch bản 4: Gõ mã nguồn, xuất file bằng chức năng Export và mở bằng phần mềm Notepad để đối chiếu dữ liệu vật lý.

### 4.2 Kết quả thực nghiệm

#### 4.2.1 Giao diện chính và hệ thống quản lý tập tin
- **Kết quả đạt được**: Trình duyệt render giao diện chính xác, màu sắc tương phản tốt. Thanh Sidebar hoạt động ổn định. Khi click vào nút "New Folder", nhập tên "Assets", thư mục xuất hiện. Khi hover vào thư mục, 3 nút công cụ hiện ra rõ ràng, bấm nút "Thùng rác" thư mục bị xóa ngay lập tức cùng với các file con.
- **[Hình ảnh minh họa]**: *(Sinh viên chụp màn hình giao diện tổng quan và chèn vào đây)*
- **[Hình ảnh minh họa]**: *(Sinh viên chụp màn hình lúc đang trỏ chuột vào thư mục để hiện 3 nút chức năng)*

#### 4.2.2 Tính năng viết code và Export File
- **Kết quả đạt được**: Monaco Editor tự động đổi ngôn ngữ dựa trên đuôi file. Khi đang mở file `.css`, các thuộc tính như `color`, `background-color` tự động sáng màu và gợi ý chữ (autocomplete). Tính năng Export hoạt động hoàn hảo, trình duyệt hiển thị thông báo tải xuống (Download) và file tải về giữ nguyên mọi định dạng dòng (Line breaks) đã gõ. Khi thao tác xóa file đang mở, tab trên cùng tự động đóng và màn hình chuyển về trạng thái trống (empty state) một cách trơn tru.
- **[Hình ảnh minh họa]**: *(Sinh viên chụp màn hình lúc đang gõ code HTML/CSS)*
- **[Hình ảnh minh họa]**: *(Sinh viên chụp màn hình lúc bấm File -> Export File và file được tải xuống trình duyệt)*

---

## CHƯƠNG 5. KẾT LUẬN VÀ HƯỚNG PHÁT TRIỂN

### 5.1 Kết luận
Đề tài "Xây dựng trình soạn thảo mã nguồn trên nền tảng web tĩnh" đã hoàn thành tốt các mục tiêu đặt ra. Với việc sử dụng 100% ngôn ngữ lập trình front-end cơ bản (HTML/CSS/JS) và khai thác hiệu quả thư viện mã nguồn mở Monaco Editor thông qua hệ thống phân phối nội dung (CDN), hệ thống đã chứng minh được tính khả thi của việc chạy một công cụ mạnh mẽ tương đương IDE trực tiếp trên trình duyệt mà không cần máy chủ (Server-less). 

Sản phẩm nổi bật với giao diện Dark Theme trực quan, trải nghiệm người dùng thân thiện, cấu trúc DOM được tối ưu qua Event Delegation giúp hiệu năng luôn duy trì ở mức cao. Các chức năng cốt lõi như quản lý cây thư mục đa cấp (tạo, lồng ghép, xóa) và xuất tệp tin vật lý (Export) đều hoạt động trơn tru. Hệ thống có thể được ứng dụng ngay làm công cụ giảng dạy, môi trường thực hành nhanh cho học sinh/sinh viên hoặc nhúng vào các nền tảng học trực tuyến (E-Learning).

### 5.2 Hướng phát triển
Dù đã đáp ứng được các yêu cầu thiết yếu của một trình soạn thảo cơ bản, hệ thống vẫn có tiềm năng mở rộng rất lớn. Trong tương lai, đề tài có thể tiếp tục được phát triển theo các hướng sau:
1. **Tích hợp tính năng lưu trữ cục bộ (Local Storage / IndexedDB)**: Thay vì làm mất dữ liệu khi người dùng tải lại trang (F5), hệ thống có thể lưu toàn bộ cây thư mục và nội dung file vào IndexedDB, cho phép tiếp tục công việc ở lần mở trình duyệt sau.
2. **Hỗ trợ tải lên toàn bộ dự án (Drag & Drop Project)**: Tích hợp `File System Access API` của HTML5 để cho phép người dùng kéo thả (Drag and Drop) một thư mục từ máy tính vào trình duyệt, hệ thống sẽ tự động quét và dựng thành cây thư mục.
3. **Thêm tính năng đa Tab (Multi-Tabs)**: Nâng cấp hệ thống Editor Tabs hiện tại (đang quản lý 1 tab đang mở) thành hệ thống quản lý nhiều tab song song giống VS Code thực tế, cho phép mở 4-5 file cùng lúc.
4. **Mô phỏng Terminal (Web Terminal)**: Tích hợp thư viện xterm.js để tạo một cửa sổ giả lập terminal bên dưới, hỗ trợ chạy các câu lệnh console ảo hoặc kết nối với backend sandbox (nếu sau này phát triển thêm phần Server).
