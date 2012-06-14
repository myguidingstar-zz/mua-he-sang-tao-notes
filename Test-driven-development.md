# Test Driven Development (TDD), why?
(Lưu ý:

  - Tài liệu này được tôi viết với tư cách là một nhà thực hành. Mục đích chủ yếu là phân tích tính ưu việt của TDD với hi vọng giành được sự đồng tình của các nhà quản lí, người dạy và người học.
  - Quy trình được giới thiệu sau đây không quá phức tạp, tuy nhiên nó đòi hỏi phải **hiểu đúng** và thực hiện nghiêm túc: một nguyên tắc bị làm trái sẽ giống như vào phòng mổ với **một** trong các dụng cụ phẫu thuật chưa vô trùng!
  - Sẽ có người muốn lướt nhanh để tìm một danh sách dạng "làm thế nào". Nhưng đáng tiếc tôi không thể viết các hướng dẫn "cầm tay chỉ việc" hơn được, vì:
    + Có quá đa dạng các ngôn ngữ lập trình (và kéo theo đó là các test framework).
    + Tài liệu là một bài viết, tức là việc **giao tiếp một chiều**, do đó không có cách nào để đảm bảo người thực hành không vô tình "bỏ bớt" một quy trình, trong khi việc đó dẫn đến mất ngay hiệu quả và tâm lí chán nản.
    + Bài viết không tham vọng diễn đạt bằng chữ nghĩa thứ mà người ta cần khoảng **một giờ đồng hồ thực hành để hiểu** và nhiều ngày tháng để ghi nhớ.
    + Việc thống nhất được cái "vì sao" quan trọng hơn, còn "làm thế nào" nên là phần việc chính của người học. Chỉ có hiểu bản chất mới giúp bạn đi đúng đường.
    + Quy trình TDD đứng riêng rẽ (không thực hành, không lí giải) **trông rất ngớ ngẩn! :)**
  - Để sử dụng thành thục TDD cũng đòi hỏi một thời gian để thay đổi thói quen.
    + Hãy thường xuyên đối chiếu những gì bạn làm với tài liệu này, điều chỉnh dần cho đến khi không còn "phạm quy"!
    + Xem mục "Nếu bạn chưa thành công, đừng ngần ngại!")

# Trước khi bắt đầu...
## Câu chuyện từ ngành y
Khi nghe ai đó nói họ vừa đi gặp bác sĩ, bạn sẽ hình dung ngay một chu trình:

  - Bệnh nhân trình bày về tình trạng sức khoẻ và nguyện vọng của mình.
  - Bác sĩ đo huyết áp nhịp tim, làm xét nghiệm và thậm chí siêu âm, chiếu chụp v.v...
  - Bác sĩ kết luận bệnh tình và cho phác đồ điều trị.
  - Bệnh nhân làm theo hướng dẫn, hàng ngày đều được khám thêm và do đó phác đồ điều trị có thể được điều chỉnh/thay đổi cho phù hợp.
  - Kết thúc đợt điều trị, bác sĩ khám tổng thể cho bệnh nhân để kết luận bệnh nhân đã lành bệnh.

## Một câu chuyện khác
Một ngày kia, có một người bạn kể cho bạn một câu chuyện khác:

> Tớ vừa từ bệnh viện về. Tay bác sĩ nghe tớ kể về bệnh tình xong không khám xét gì mà đưa cho tớ một đơn thuốc và tống tớ vào phòng điều trị. Tớ không thấy mặt hắn cho đến tận khi đợt điều trị kết thúc. Sau đó tớ nhận được một kết luận "Còn chạy được" đủ để ra viện. Ơn trời là tớ còn sống!

Bạn sẽ phá lên cười:

> Bạn thân mến, bạn đọc quá nhiều Azit Nexin rồi. Làm gì có cái chuyện khôi hài đó. Dù ở những bệnh viện quá tải nhất Việt Nam thì **người ta vẫn khám trước khi cho thuốc**!

Bạn có thể nghĩ tôi đang kể một câu chuyện cười quá lố. Vâng, tôi nghĩ câu chuyện trên đây không có ở bất kì bệnh viện nào. Tuy nhiên, những **câu chuyện tương tự** lại đang diễn ra rất phổ biến trong ngành CNTT của chúng ta: việc kiểm thử (nghĩa hẹp mà từ "test" đang được hiểu) chỉ được thực hiện sau khi chương trình viết hoàn chỉnh!

Phải chăng vì ngành CNTT không có những "lời thề Turing"[1], "lời thề Church"[2] nên chúng ta **không đủ nghiêm túc** khi phát triển phần mềm?

[1],[2]: [Alan Turing](http://en.wikipedia.org/wiki/Alan_Turing) và [Alonzo Church](http://en.wikipedia.org/wiki/Alonzo_Church) là những người sáng lập ra khoa học máy tính. Câu nói ngầm so sánh với "Lời thề Hippocrates" của ngành y.

# Có một cách làm khác!
## Test trước hay test sau?
"Test trước" là dấu hiệu quan trọng của TDD. Quy trình đầy đủ sẽ là "test trước, trong và sau". Mô hình "ba test" này gọi là Test-Driven Development (TDD).

> TDD = TFD + Refactor

(Các khác niệm sẽ được giải thích cụ thể trong bài viết về Quy trình. Nhưng bạn chưa cần đọc chúng ngay đâu!)

Trong thực tiễn phát triển phần mềm, test dần thể hiện được vai trò của nó. Năm 1994, [Kent Beck](http://en.wikipedia.org/wiki/Kent_Beck) viết test framework đầu tiên cho môi trường ngôn ngữ [SmallTalk](http://en.wikipedia.org/wiki/Smalltalk). Với ưu thế rõ rệt, TDD nhanh chóng được tiếp thu và hầu như các ngôn ngữ lớn trên thế giới đều đã có test framework của mình. Ngày nay, TDD đã trở thành một **chuẩn mực** trong việc phát triển phần mềm.

> TDD được hiểu là việc phát triển phần mềm có sự tham gia (nếu không muốn nói là đóng vai trò định hướng) chặt chẽ của test. Về mặt triển khai, TDD là mô thức phát triển phần mềm đã được **quy trình hoá**.

# Test Driven Development v.s tư duy cũ
Trước khi bắt đầu, hãy nhớ khái niệm test trong TDD đã **được mở rộng** hơn so với lập trình truyền thống.

## Phân biệt test với dò lỗi (bug)
  - Công đoạn test trong "test sau" (lập trình truyền thống) là việc sau khi viết xong toàn bộ, người ta đưa chương trình vào môi trường production (môi trường làm việc thật) hoặc mô phỏng để chạy thử xem có phát sinh lỗi hay không.
  - "Test trước": khi bạn viết xong phần tử test đầu tiên (nó sẽ fail!) là khi bạn hiểu và trình bày được **yêu cầu của bài toán**.
  - TDD (TFD + Refactor) chính là việc viết nháp với những dấu chấm lửng. Trong quá trình bạn viết test, bạn sẽ **"nháp" và "xoá nháp"** đi nhiều lần. Chỉ sau vài lượt như vậy, bài toán và thiết kế lời giải của bạn tiến rất gần đến mức thực tế!

## Tư duy giải quyết vấn đề
Hiểu "test" theo nghĩa rộng của nó trong TDD, bạn sẽ không còn thấy nó ngược đời nữa. Trái lại, TDD còn rất tự nhiên, vì đó là quy trình được thiết kế **cho con người**:

  - Khi gặp một **bài toán của cuộc sống**, tư duy thông thường để giải quyết sẽ lần lượt qua các bước:
    + Bước 1: Phân tích vấn đề và đưa ra yêu cầu (tức kết quả muốn đạt được)
    + Bước 2: Phương hướng giải chung nhất (Trong lập trình: thường được thể hiện lại trên các sơ đồ UML)
    + Bước 3: Cho ra lời giải cụ thể bằng ngôn ngữ tự nhiên hay trừu tượng (Concept)
    + Bước 4: Thao tác (Trong lập trình: thể hiện lại lời giải trên bằng ngôn ngữ máy tính)
  - Hầu hết mọi người sẽ đồng tình với các bước trên, nhưng đến khi bắt tay vào việc thì không phải ai cũng làm như vậy. Bước thao tác luôn là bước tốn nhiều thời gian nhất. Chính vì thế nhiều người bị **sa đà vào bước này**.
    + Với các bài toán nhỏ, chẳng hạn như việc giao tiếp hàng ngày, 3 bước đầu diễn ra ngay trong vô thức. Khi các bài toán lớn hơn, nhất là khi nó trở thành một dự án tốn nhiều tháng thậm chí nhiều năm triển khai, thời gian cho 3 bước đầu lại không được **nhân lên với tỉ lệ tương xứng**!
    + Hãy nhớ: Nếu chỉ để ngốn thời gian, bước 4 không cần đến kết quả của 3 bước trước :) Thiếu đi chúng, nhà phát triển có xu hướng làm "thứ mình có (thể)" thay vì "thứ họ/mình cần".
    + Không có mục tiêu, chúng ta luẩn quẩn trong "giới hạn kĩ thuật" mà mình tự đặt ra, hoặc mải mê "đột phá sáng tạo" ở một nơi không cần thiết. Theo đó, sản phẩm cuối cùng rất có thể sẽ là một con quái vật :)

## Tiết kiệm thời gian?
Sẽ có người cho rằng:

> Với TDD tôi phải viết thêm cả test nữa, làm sao nói là tiết kiệm thời gian hơn được?

  - Việc viết "test trước" như đã nói, đóng vai trò như viết nháp. Khi không làm như vậy, bạn vẫn mất thời gian cho việc suy nghĩ trong đầu, chỉ là chi phí thời gian này đã **không được tính** vào tổng chi phí thôi.
  - Quá trình thể hiện ra ngôn ngữ máy tính chắc chắn phải đi qua những "non-computable functions"[1], trong đó có những thành phần phức tạp. Biết rõ tổng quan (3 bước đầu) giúp chúng ta có thể lựa chọn một trong các phương án:
    + tìm kiếm các thư viện sẵn có (thế mạnh của nguồn mở là đây!)
    + thuê ngoài một bên thứ ba triển khai
    + thành lập đội chuyên trách

[1]:
  - Một ví dụ cho "non-computable functions" (mặc dù không được điển hình lắm) để dễ hình dung trong điều kiện Việt Nam là  "(trong một dự án web) in ra `tiêu đề`, `nội dung`, `tác giả` của một `bài viết` với giao diện thân thiện". Để hiện thực hoá thao tác này sẽ phải có đoạn chương trình làm thao tác in ra mã HTML, phải có người viết CSS, thậm chí động đến đồ hoạ và ajax!
  - Các ví dụ điển hình hơn cho "non-computable functions" thường là các đoạn chương trình cần một thuật toán để xử lí. Chẳng hạn "tự động in ra danh sách các `bài viết` có liên quan" sẽ đòi hỏi phải xây dựng một thuật toán phân tích nội dung của các bài viết. Nhưng nếu như nguồn lực có hạn thì thuật toán có thể chỉ là tính toán số thuộc tính `từ khoá` chung.

> Khẩu hiệu của ngành CNTT là "Nothing is impossible!", nhưng chọn cái impossible nào để hiện thực hoá thì cần phải thực tế.

## Phòng bệnh hơn chữa bệnh
  - Với việc sử dụng TDD kết hợp với functional programming style, nhà phát triển có thể **tránh được hầu hết** lỗi khi chương trình được viết xong! Lập trình viên tuân thủ quy trình TDD sẽ không **mất phần lớn thời gian** cho việc dò lỗi giống như các đồng nghiệp truyền thống.

> - Để hiểu giá trị của việc **làm rõ yêu cầu**, hãy hỏi những người đã đầu tư cả triệu USD vào một mặt hàng không bán được.
> - Để hiểu giá trị của việc **vạch ra hướng giải chung**, hãy hỏi những người hàng ngày tham gia giao thông Hà Nội về quy hoạch đô thị.
> - Để hiểu giá trị của việc **refactor**, hãy hỏi người đã bỏ tiền ra mua những "[chung cư cao cấp](http://vef.vn/2012-05-01-chung-cu-cao-cap-nhanh-xuong-cap)" về chất lượng sống!

## Tài liệu cho nhà phát triển
  - Các nhà phát triển thường khoái đọc code và những ví dụ hơn là gặm nhấm tập tài liệu giải thích các vấn đề kĩ thuật bằng ngôn ngữ phi kĩ thuật (như bài viết này đang làm ^^). TDD làm **chính xác** công việc đó!
  - Thêm một vài comment trước mỗi test nếu cần, bạn đã có tài liệu hướng dẫn cho các nhà phát triển khác (và cho chính bạn!). Quả là "nhất cử lưỡng tiện".
  - Tất nhiên cần phân biệt tài liệu cho nhà phát triển và cho người sử dụng. Tài liệu cho nhà phát triển cũng cần có hướng dẫn tổng quan, phương pháp luận, quy ước v.v... nữa.

# Kết luận
## Tóm tắt
  - TDD là công cụ cho nhà phát triển chuyên nghiệp, giúp nâng cao năng suất thông qua:
    + Hiểu đúng bài toán
    + Hướng vào mục tiêu rõ ràng, tránh được việc viết những đoạn chương trình thừa
    + Các thành phần của chương trình làm đến đâu chắc chắn đến đấy -> khả năng bảo trì, mở rộng và kế thừa cao.
  - Các lợi ích khác:
    + Làm ví dụ minh hoạ cho nhà phát triển
    + Phối hợp tốt với Agile, functional programming style, hệ thống Quản lí phiên bản.

## Thực hành
  - Để hướng tới sự chuyên nghiệp, người học CNTT nên biết TDD càng sớm càng tốt.
  - Đọc thêm tài liệu về TDD và tài liệu một test framework nào đó của ngôn ngữ lập trình bạn đang học/dùng **bằng tiếng Anh**.
  - Tìm hiểu thêm về TDD trên các trang video và presentation:
    + `tdd`
    + `tdd examples + <your programming language>`
  - Tham gia một dự án nguồn mở có sử dụng TDD mà bạn thích nhưng cần xem kĩ hướng dẫn (guideline) và trao đổi với những developer có kinh nghiệm trong dự án. (Bạn không cần chuẩn bị gì nhiều, ngoại trừ tinh thần học hỏi!)

## Nếu bạn chưa thành công, đừng ngần ngại!
  - Với TDD chúng ta không nên nóng vội:
    + Ngay cả Microsoft cũng từng có [hướng dẫn về TDD](http://jamesshore.com/Blog/Microsoft-Gets-TDD-Completely-Wrong.html) cho lập trình viên hết sức lệch lạc (2004)!
  - Trong điều kiện thực tế ở Việt Nam, tổ chức của bạn có thể chưa có đủ điều kiện về mặt nhân sự để triển khai TDD hoặc công việc hàng ngày khiến bạn chưa đủ thời gian để **đi đến tận cùng** của TDD. Trong trường hợp đó, xin vui lòng không để trải nghiệm cá nhân của bạn (nhất là đừng nói dối rằng bạn/tổ chức của bạn đang tiến hành TDD rất tốt!) ảnh hưởng đến **quyền được biết** và lựa chọn của những người có cơ hội học tập.
  - Tài liệu này không nên đơn giản là đọc từ trên xuống, hay lướt qua để tìm quy trình. Hãy thoải mái "nhảy cóc" giữa các phần và thậm chí là đọc lại nhiều hơn một lượt để hiểu được các thành phần.

# Bản quyền
  - Khi đăng tải lại bài viết này, vui lòng đăng tải cả thông tin bản quyền dưới đây
<br /><a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/3.0/vn/"><img alt="Creative Commons License" style="border-width:0" src="http://i.creativecommons.org/l/by-nc-nd/3.0/vn/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/Text" property="dct:title" rel="dct:type">Test Driven Development (TDD), why?</span> by <span xmlns:cc="http://creativecommons.org/ns#" property="cc:attributionName">Hoàng Minh Thắng (myguidingstar)</span> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/3.0/vn/">Creative Commons Attribution-NonCommercial-NoDerivs 3.0 Vietnam License</a>.
