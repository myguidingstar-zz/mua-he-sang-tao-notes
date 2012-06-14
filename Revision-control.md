# Quản lí phiên bản (Revision Control hay Version Control)
(Lưu ý:

  - Đây là một bài viết giới thiệu chung nhất về quản lí phiên bản.
  - Bài viết hướng đến đông đảo người đọc: bạn **không bắt buộc phải biết về CNTT** để hiểu bài viết này.
  - Bạn không bắt buộc phải đọc hết ngay bài viết mà có thể lướt qua các chủ đề mình quan tâm. Cuối bài có phần tổng kết cho những ai muốn có kết luận nhanh.
  - Những ai muốn tìm hiểu sâu hơn nên tiếp cận các tài liệu tiếng Anh với mục "Đọc thêm" ở cuối bài.)

## Quản lí phiên bản là gì? Nó có cần thiết không? Nó có khó học không?
Có vẻ như Quản lí phiên bản (Revision Control/Version Control) không mấy phổ biến ở Việt Nam, phải chăng đây là một thứ rất hi-tech, làm những công việc hết sức phức tạp và cao siêu? Ai đó có thể thốt lên: cả đời tôi chưa bao giờ động đến thứ đó! Vậy liệu rằng Quản lí phiên bản có phải là việc riêng của lập trình viên? Hãy thử cùng nhau xem một vài ví dụ:

### Các phiên bản (Versions/Revisions)
Có nhiều phiên bản khác nhau của cùng một đối tượng là một nhu cầu hết sức tự nhiên. Chúng ta sẽ muốn giữ mỗi trạng thái khác nhau đó để mang ra dùng cho từng thời điểm cụ thể. Lục tìm trong máy mỗi người có thể thấy những tên file (các "phiên bản") đại loại như:

  - diễn-văn-tẻ-nhạt_2010.txt
  - diễn-văn-tẻ-nhạt_2011.txt
  - diễn-văn-tẻ-nhạt_2012.txt
  - thư-tình_gửi-Đào.odt
  - thư-tình_gửi-Lê.odt
  - thư-tình_gửi-Mận.odt ;)
  - bản-thiết-kế_đang-tốt.svg
  - bản-thiết-kế_thử-nghiệm.svg

Cách quản lí đơn giản ở trên vẫn thường được chúng ta thực hiện dễ dàng bằng thao tác `File` -> `Save As...` trong các chương trình máy tính.

### Ghi lại sửa đổi
Đây là một chức năng thường được sử dụng và sẵn có trong các bộ phần mềm văn phòng như [LibreOffice](http://www.libreoffice.org/), [OpenOfice](http://www.openoffice.org/), [GoogleDocs](http://docs.google.com/)... trong đó người dùng có thể bật chế độ xem những thay đổi mà mình (và người khác) đã làm ngay trên file đó. Chức năng này cũng quen thuộc với những ai hay viết blog bằng [Wordpress](http://www.wordpress.org), hay viết/sửa bài trên một trang Wiki bất kì.

Có thể thấy, quản lí phiên bản là một việc làm hết sức gần gũi, và vẫn đang được áp dụng rộng rãi không chỉ trong lập trình. Tuy nhiên, cùng với thời gian, khi khối lượng các công việc tăng lên về quy mô và độ phức tạp thì yêu cầu về quản lí phiên bản cũng cao hơn. Đó là lí do ra đời các công cụ phục vụ việc quản lí các phiên bản một cách hoàn chỉnh, gọi là các "Hệ thống Quản lí phiên bản" (Revision/Version Control System). Chúng được ứng dụng nhiều nhất trong việc quản lí mã nguồn và quản lí tài liệu.
## Hệ thống Quản lí phiên bản (Revision/Version Control System)
### Chức năng
Các Hệ thống Quản lí phiên bản (sau đây gọi là RCS) cung cấp **đồng thời** ba chức năng quan trọng nhất:

  - Chức năng phục hồi: cho phép khôi phục trạng thái trước khi phát hiện ra có lỗi trong một thao tác sửa đổi đã làm.
  - Chức năng đồng bộ: cho phép nhiều người cùng sửa một/một tập hợp file cùng lúc vì các thao tác sửa đổi gây xung đột có thể được phát hiện và giải quyết sau đó.
  - Ghi lại lịch sử: ghi lại các thông tin cần thiết của từng sửa đổi một, như tác giả, thời gian, các ghi chú giải trình thao tác thay đổi đó v.v...

Chúng ta cùng tìm hiểu chi tiết hơn về các RCS:

### Đơn vị cơ bản của RCS: commit
  - Commit là thao tác ra lệnh cho RCS ghi lại những thay đổi (change-sets) mà tác giả vừa thực hiện với (các) file mà RCS đang theo dõi. Commit cũng được dùng với nghĩa là những thay đổi nằm trong cùng một lần "commit" (ra lệnh) này. "Những thay đổi" ở đây có thể là tạo file, đổi tên/di chuyển, xoá file, sửa đổi nội dung v.v...
  - Để các commit có giá trị thông tin (xem lại sau này chẳng hạn), ngoài thông tin tác giả và thời gian được RCS tự động thêm vào, người sử dụng phải nhập các ghi chú (comment) lí giải về commit đó. Các ghi chú của commit được gọi là "commit message". Các message nên ngắn gọn, giải thích xem những sửa đổi đó nhằm làm gì (và khái quát cách làm nếu nó phức tạp).
  - Khi cần xem lại các commit trước đó, người ta gọi một cái gọi là "commit history" hay lịch sử commit.

### Thao tác sửa đổi nội dung: patch và diff
  - So với việc lưu lại từng phiên bản, việc **chỉ lưu những phần thay đổi** có lợi hơn cho không gian đĩa, cũng như giúp cho việc trao đổi các thay đổi trong môi trường mạng máy tính nhanh hơn. Thao tác "diff" sẽ tự động **phân tích hai phiên bản khác nhau** của một file để chỉ ra phần khác nhau (diff). Phần khác nhau này có thể được xuất ra thành một file gọi là "patch" chứa **thông tin về thay đổi theo quy chuẩn**.
  - Cần lưu ý là patch với nghĩa là "bản vá" chỉ là một ứng dụng cụ thể của patch. Thao tác applying patch nói chung là "từ file trước sửa đổi và bản patch tổng hợp thành file sau sửa đổi".
  - Các thao tác diff và patch có thể thực hiện trực tiếp thông qua các lệnh cùng tên trên các hệ thống GNU/Linux hoặc gián tiếp nhờ sự giúp đỡ của các RCS.

### Xung đột (conflict) giữa các commit
  - Xung đột (conflict) giữa các commit xảy ra khi có hai (hay nhiều hơn) commit độc lập với nhau xuất phát từ cùng một commit cũ trước đó. Xung đột thường xảy ra khi có một trong các commit mới đó chứa thao tác xoá bỏ. Trường hợp các commit đều là thao tác thêm sẽ dễ dàng được các RCS tự động xử lí (resolve). Khi xung đột xảy ra, lập trình viên phải cho RCS biết kết quả cuối cùng mà mình mong muốn.

## Hai dạng Hệ thống Quản lí phiên bản chính: tập trung và phân tán
### Dạng tập trung (Centralized Version/Revision Control)
Ví dụ điển hình cho dạng này là CVS và SVN. Đặc điểm của dạng này là hệ thống làm việc theo mô hình client - server trong đó server (kho mã nguồn) đặt một nơi và cho phép các client kết nối đến nó.

### Dạng phi tập trung (Decentralized/Distributed Version/Revision Control)
Các hệ thống thuộc dạng này ra đời muộn hơn. Trong mô hình của các hệ thống này, mỗi người sử dụng có bản sao của **toàn bộ** kho mã nguồn (repository), bao gồm cả tập hợp các file và lịch sử sửa đổi. Trong các hệ phi tập trung các kho mã nguồn đồng bộ với nhau bằng cách trao đổi các commit dưới dạng các patch. Hai hệ thống quản lí phiên bản phân tán phổ biến nhất hiện nay là Git và Mercurial.
Sự khác biệt quan trọng so với các hệ tập trung là:

  - Các kho mã nguồn (trên máy của lập trình viên chẳng hạn) hoàn toàn độc lập, do đó các thao tác hay dùng như commit, xem history, phục hồi (reverting changes) có thể thực hiện tại chỗ (local) mà không cần kết nối đến server tập trung.
  - Tương tác giữa các kho mã nguồn chỉ cần thiết khi một kho mã nguồn muốn gửi/nhận các thay đổi (pushing/pulling changes) với một kho khác.
  - Mỗi kho mã nguồn là một bản sao đầy đủ của toàn bộ mã nguồn. Điều này giúp tránh được nguy cơ mất dữ liệu.
Lưu ý là vẫn có thể quy ước một kho mã nguồn đóng vai trò trung tâm trao đổi để đảm bảo dữ liệu được truyền tải đầy đủ đến các kho thành viên. Đó là cách chúng ta vẫn làm với các kho trên github, bitbucket, google-code v.v...

## Chiến lược cho việc sửa đổi: Thay đổi theo từng bước lớn hay nhỏ? (Big steps/small steps?)
Nhiều người nghĩ rằng nên "để dành" các thay đổi đến khi "đáng kể" rồi mới commit một lượt. Trên thực tế, chiến lược này không tiết kiệm thời gian như họ tưởng.

  - Một trong các lợi ích của commit là nhanh chóng phục hồi (revert) lại trạng thái từ commit trước đó. Việc để dồn cho thay đổi đáng kể (big steps) không mang lại thêm "cái được" nhưng lại làm tăng đáng kể "cái mất". Làm theo hướng này, khi gặp lỗi trong quá trình thử nghiệm (vốn là một việc rất thường xuyên), lập trình viên phải lựa chọn hoặc mất cả (revert lại ngay), hoặc loay hoay sửa đến lúc được thì thôi. Dù chọn cách nào thì đó cũng là sự lãng phí (thời gian, công sức) mà lẽ ra có thể tránh được khi commit theo từng bước nhỏ.
  - Chiến lược small steps giúp lịch sử commit chi tiết, đồng thời các commit message cũng đơn giản và tự nhiên (ghi lại suy nghĩ của lập trình viên ngay tại thời điểm viết). Trong khi đó với chiến lược big steps, các commit message phức tạp hơn, và việc phải lục lại trí nhớ có thể khiến lập trình viên chán nản mà tạo ra những message nghèo giá trị thông tin. Big steps tạo ra lịch sử commit nghèo nàn và "quan liêu".
  - Nhiều RCS còn cho phép hợp nhất các thay đổi nhỏ. Điều này có thể hữu ích cho việc duyệt xem lịch sử được gọn hơn. Lưu ý chỉ áp dụng thao tác hợp nhất này cho những bộ phận mã nguồn đã đi vào ổn định. Nói chung, việc sửa đổi lịch sử cần có sự cân nhắc kĩ lưỡng.
  - Chiến lược big steps còn dẫn đến sự kém linh hoạt: các xung đột (conflict) phức tạp và việc xử lí xung đột cũng khó khăn gấp nhiều lần.

Tóm lại, chiến lược big steps chỉ có thể gắn với các RCS tập trung vốn thống trị trong quá khứ chủ yếu do hạ tầng máy tính và mạng còn hạn chế.

## Một số thuật ngữ khác:
  - branch: rẽ nhánh
  - merge (merging branches): sáp nhập hai nhánh lại
  - mainline/trunk/master branch: nhánh chính
  - label/tag: nhãn/thẻ

Các thuật ngữ này cũng sẽ được bắt gặp khi thao tác thực tế. Mỗi hệ thống quản lí phiên bản khác nhau có thể sử dụng các thuật ngữ khác nhau. Việc hiểu các thuật ngữ trên **đòi hỏi một quá trình thực hành**. Trong khuôn khổ bài viết, tôi không thể đi sâu hơn. Muốn biết cụ thể, người đọc phải xem tài liệu cụ thể của hệ thống quản lí phiên bản mà mình lựa chọn.

## Lựa chọn hệ thống quản lí phiên bản
Có nhiều hệ thống quản lí phiên bản và chúng rất khác nhau từ quan điểm thiết kế đến cách thức vận hành. Chúng ta phải có lựa chọn khi bắt đầu dự án mới, hoặc khi rà soát lại hệ thống đang sử dụng và quyết định xem có nên chuyển đổi hay không. Việc lựa chọn trước hết cần dựa trên việc trả lời câu hỏi: Thế nào là một hệ thống quản lí phiên bản tốt?

### Hệ thống quản lí phiên bản tốt
  - Hệ thống quản lí phiên bản trước hết phải đảm bảo ba chức năng cơ bản (xem mục **Chức năng** ở trên) hoạt động dễ dàng và thuận tiện.
  - Một hệ thống quản lí phiên bản cần khuyến khích người sử dụng commit (khuyến khích đổi mới sáng tạo), bằng cách:
    + Tối thiểu hoá chi phí (thời gian, công sức) trong từng commit.
    + Khuyến khích commit tốt và message tốt
  - An toàn dữ liệu: có thể back-up thường xuyên, nhưng tốt nhất là dùng mô hình phân tán.
  - Kiểm soát chất lượng commit: Ngoài vấn đề chất lượng mã nguồn, luôn rình rập nguy cơ kẻ xấu chèn thêm các đoạn mã độc. Việc kiểm soát này chỉ có thể thực hiện khi:
    + chỉ có ai có quyền được commit, không được mạo danh (với trường hợp mã nguồn không công khai)
    + việc theo dõi các thay đổi trong từng commit phải dễ dàng, trực quan.
  - Ngoài ra còn phải xem xét khả năng tích hợp với các phần mềm khác, các công cụ hỗ trợ v.v...

Với đặc điểm thường xuyên làm việc với khối lượng mã nguồn khổng lồ, yêu cầu về đồng bộ hoá cao, cộng đồng phần mềm Tự do nguồn mở luôn đi đầu về Hệ thống quản lí phiên bản. Các đại diện ưu tú của phần mềm Tự do nguồn mở trong lĩnh vực này là git và mecurial.

### Hệ thống quản lí phiên bản phù hợp
  - Đặc thù của việc phát triển phần mềm là việc sửa đổi các file mã nguồn diễn ra thường xuyên, liên tục. Chính vì vậy, hệ thống quản lí phiên bản được sử dụng ảnh hưởng mạnh mẽ đến hiệu quả và chất lượng của quá trình phát triển phần mềm. Vì vậy cần **dứt khoát** với các hệ thống quản lí phiên bản gây ra năng suất kém. Việc mạnh dạn chuyển đổi sang những công nghệ có lợi cũng thể hiện **năng lực** của bạn và tổ chức của bạn. Đó chỉ còn là vấn đề thói quen, khi mà các hệ RCS mới **đều hỗ trợ chuyển đổi (migrate)** từ các hệ thống khác một cách tiện lợi.
  - Các hệ RCS tốt tương đối giống nhau, việc lựa chọn trong số chúng chỉ còn dựa trên sự tương đồng về phong cách trong tổ chức. Nếu trong tổ chức của bạn đã có một số thành viên quen làm việc với một RCS tốt thì điều đó quả là tuyệt vời!

# Kết luận
## Tóm tắt
  - Sử dụng các Hệ thống quản lí phiên bản (RCS) là tất yếu với những ai muốn làm việc chuyên nghiệp.
  - Chiến lược tạo ra các thay đổi nhỏ, liên tục ưu việt hơn chiến lược tạo ra các thay đổi lớn, đứt quãng.
  - Các hệ thống RCS phân tán có lợi thế hơn các hệ tập trung.
  - Các RCS hiện đại như git, mercurial rất dễ sử dụng và hội tụ nhiều ưu điểm.

## Khuyến nghị
  - Dùng các RCS từ những giây đầu tiên của một dự án mới.
  - Nên sớm chuyển đổi từ các RCS có nhiều hạn chế như CVS, SVN sang các RCS như git, mecurial...
  - Với những người thường xuyên viết tài liệu, việc sử dụng các Hệ thống quản lí phiên bản cũng rất có ích. Nên lựa chọn các tài liệu có định dạng nguồn là văn bản thuần (plain text) như [Latex](http://www.latex-project.org/), [markdown](http://daringfireball.net/projects/markdown/)... Nếu buộc phải dùng các định dạng khác, hãy sử dụng các định dạng mở như [OpenDocumentFormat](http://en.wikipedia.org/wiki/OpenDocument) để có thể sử dụng kết hợp với RCS (và đảm bảo khả năng kết hợp rộng rãi nói chung). Một [hướng dẫn](http://www-verimag.imag.fr/~moy/opendocument/) cho việc kết hợp này.

## Đọc thêm
  - Tài liệu về [git](http://git-scm.com/documentation)
  - Tài liệu về [mercurial](http://mercurial.selenic.com/)

# Bản quyền
  - Khi đăng tải lại bài viết này, vui lòng đăng tải cả thông tin bản quyền dưới đây
<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/3.0/vn/"><img alt="Creative Commons License" style="border-width:0" src="http://i.creativecommons.org/l/by-nc-nd/3.0/vn/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/Text" property="dct:title" rel="dct:type">Quản lí phiên bản (Revision Control hay Version Control)</span> by <span xmlns:cc="http://creativecommons.org/ns#" property="cc:attributionName">Hoàng Minh Thắng (myguidingstar)</span> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/3.0/vn/">Creative Commons Attribution-NonCommercial-NoDerivs 3.0 Vietnam License</a>.
