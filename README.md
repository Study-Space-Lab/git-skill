<p align="center">
	<img src="./img/Git-Icon.png" alt="git-icon" height="256px" width="256px">
</p>

# Mục lục

- [Mục lục](#mục-lục)
- [VCS và Git](#vcs-và-git)
	- [VCS là gì?](#vcs-là-gì)
	- [Tại sao lại cần nó?](#tại-sao-lại-cần-nó)
	- [Phân loại VCS](#phân-loại-vcs)
	- [Git là gì?](#git-là-gì)
	- [Cơ chế hoạt động?](#cơ-chế-hoạt-động)
	- [Dữ liệu lưu trữ trong Git đảm bảo tính toàn vẹn](#dữ-liệu-lưu-trữ-trong-git-đảm-bảo-tính-toàn-vẹn)
	- [Git có lợi ích gì?](#git-có-lợi-ích-gì)
- [Cài đặt và cấu hình Git](#cài-đặt-và-cấu-hình-git)
	- [Tải Git](#tải-git)
	- [Cài đặt Git](#cài-đặt-git)
	- [Cài đặt Git trên MacOS và Ubuntu](#cài-đặt-git-trên-macos-và-ubuntu)
- [Trạng thái của Git](#trạng-thái-của-git)
- [Lệnh cơ bản](#lệnh-cơ-bản)

# VCS và Git

## VCS là gì?

**Hệ thống quản lý phiên bản - Version Control System (VCS)** là một hệ thống ghi nhận và lưu lại sự thay đổi của các file theo thời gian, từ hệ thống đó một file có thể phục hồi quay về trạng thái (phiên bản) ở một thời điểm trước đó. Ngoài ra bạn có thể theo dõi sự thay đổi của một file theo thời gian, ai đã thay đổi, thay đổi vào lúc nào,... Đồng thời, nó cũng giúp cho ta dễ dàng hợp tác làm việc với nhiều người khác trong cùng một dự án.

<p align ="center">
	<img src="./img/VCS1.png" alt="VSC Banner">
</p>

Có nhiều hệ thống VCS mà bạn có thể chọn sử dụng như: Concurrent Versions System, Subversion, Git, Mercurial,...Nổi bật trong đó là **Git**

## Tại sao lại cần nó?

Giả sử trường hợp bạn cần làm dự án theo team 3, 4 thành viên. Như vậy mỗi thành viên sẽ code một số module nhỏ, cuối cùng sẽ phải đến ngày gộp code. Có 2 trường hợp xảy ra, hoặc là team bạn phải ra quán coffee gộp code (như mình từng làm khi mới học code) hoặc team bạn sử dụng version control. Với công cụ này, mỗi thành viên team bạn có thể tạo ra 1 phiên bản riêng cho mình (branch) và làm việc độc lập trên đó, khi cần gộp code, bạn chỉ việc gộp 2 branch lại với nhau, mọi thứ đều được version control đánh dấu thời gian rõ ràng, công việc sẽ trở nên dễ dàng hơn rất nhiều.

## Phân loại VCS

**VCS Cục Bộ**

Khi bạn chưa biết đến VCS thì chắc là bạn đã từng làm việc sau: _Giả sử bạn có một thư mục chứa một số file (code, media ...), trước khi bạn sửa đổi các file đó có thể bạn sẽ copy lại thư mục và lưu lại với một cái tên đánh dấu để nhỡ cần phục hồi lại các file gốc thì có thể copy trở lại. Việc làm của bạn chính là bạn vừa vận hành một hệ thống quản lý phiên bản_. Cách làm này đơn giản tuy nhiên gây ra nhiều lỗi như bạn có thể quyên mất thư mục ban đầu lưu trữ nhất là khó mà nhớ thời điểm lưu lại khi copy nhiều lần thư mục.

Chỉ cần từ 10 thư mục trở lên thôi là bảo đảm công việc sẽ bắt đầu có sự nhầm lẫn.

Để giải quyết vấn đề này, các lập trình viên từ lâu đã phát triển nên một VCS cục bộ với một cơ sở dữ liệu đơn giản chỉ nhằm mục đích duy nhất: Lưu giữ tất cả từng phiên bản và ghi nhận các thay đổi của từng phiên bản sau đó. Hệ thống đó bạn có thể gọi là VCS cục bộ, mô hình hóa hoạt động như hình.

<p align="center">
	<img src="./img/localVCS.png" alt="local-VCS">
</p>

Công cụ nổi tiếng có thể kể đến là **RCS** (Revision Control System), vẫn còn được sử dụng ở nhiều hiện nay. Thậm chí trong các máy tính MAC OS X nó vẫn tích hợp vào các công cụ lập trình (IDE) lệnh rcs để người dùng có thể tự quản lý các phiên bản khác nhau của dự án tại từng thời điểm.

**VCS Trung Tâm**

Nhưng nếu áp dụng như cách trên vừa nói, chuyện lại nảy sinh tiếp theo là: Mình muốn chia sẻ các phiên bản dự án của mình với các đồng nghiệp khác trong cùng hệ thống (trong một công ty) thì làm thế nào? Vẫn phải tìm và copy rồi gửi cho đồng nghiệp? Việc tự quản lý các phiên bản để tránh nhầm lẫn đã giải quyết xong rồi, còn chia sẻ thế nào cho nhanh chóng lại nảy sinh.

Giải pháp VCS tập trung ra đời.

Các hệ thống này – có thể kể tên như CVS, Subversion, Perforce – đều triển khai một máy chủ chứa toàn bộ các tập tin phiên bản khác nhau của tất cả các dự án của từng người trong nội bộ công ty đang làm việc. Các đồng nghiệp này có thể truy xuất lên đây và xem của nhau đều được.

<p align="center">
	<img src="./img/centralizedVCS.png" alt="Centralized-VCS">
</p>

Cách này tỏ ra hiệu quả trong thời gian dài, khi mà nó giải quyết được cả 2 vấn đề là tổ chức, lưu trữ các phiên bản hiệu quả; chia sẻ và truy xuất các phiên bản của từng cá nhân khác nhau dễ dàng hơn.

Tuy nhiên CVCS vẫn có nhược điểm khi Sever bị dừng thì không thể kết nối các thành viên làm việc, hoặc mất dữ liệu (do ở đĩa hư hỏng) khì rất khó khôi phục lại file.

**VCS Phân Tán**

VCS phân tán sẽ giải quyết câu chuyện đau đầu trên. Có thể kể những cái tên tiêu biểu như Git, Mercurial, Bazaar hay Darcs. Ở giải pháp này, các máy truy cập tới không đơn giản chỉ tải về phiên bản mới nhất của dữ liệu, mà nó sẽ tải về toàn bộ kho chứa (Repository). Do đó, nếu có một máy chủ nào ngưng hoạt động đi nữa, thì cũng có thể truy xuất được dữ liệu dễ dàng từ một máy khác để khôi phục lại những gì đã mất.

<p align="center">
	<img src="./img/distributedVCS.png" alt="Distributed-VCS">
</p>

Điểm nổi trội khác nữa có thể kể đến, đó là các hệ thống kiểu này xử lý rất hiệu quả trong việc quản lý các Repository từ xa, nhằm giúp cho một người có thể cộng tác và làm việc với nhiều người khác nhau ở bất kỳ đâu.

**Git** chính là hệ thống quản lý phiên bản phân tán (DVCS), với các ưu điểm: tốc độ, đơn giản, phân tán, phù hợp với dự án lớn nhỏ.

## Git là gì?

**Git** là một hệ thống quản lý phiên bản phân tán (Distributed Version Control System – DVCS), nó là một trong những hệ thống quản lý phiên bản phân tán phổ biến nhất hiện nay. Git cung cấp cho mỗi lập trình viên kho lưu trữ (repository) riêng chứa toàn bộ lịch sử thay đổi.

## Cơ chế hoạt động?

Sự khác biệt chính giữa Git và bất kỳ VCS nào khác (bao gồm Subversion…) là cách Git nghĩ về dữ liệu của nó.

Về mặt khái niệm, hầu hết các hệ thống khác đều lưu trữ thông tin dưới dạng danh sách các thay đổi dựa trên file. Các hệ thống này (CVS, Subversion, Perforce, Bazaar, v.v.) coi thông tin chúng lưu giữ dưới dạng một tập hợp các file và những thay đổi được thực hiện đối với mỗi file theo thời gian.

<p align="center">
	<img src="./img/Git-hdpng.png" alt="git-hd1">
</p>

Git không nghĩ đến hoặc lưu trữ dữ liệu của mình theo cách này. Thay vào đó, Git coi thông tin được lưu trữ là một tập hợp các snapshot – ảnh chụp toàn bộ nội dung tất cả các file tại thời điểm.

Mỗi khi bạn “commit”, Git sẽ “chụp” và tạo ra một snapshot cùng một tham chiếu tới snapshot đó. Để hiệu quả, nếu các tệp không thay đổi, Git sẽ không lưu trữ lại file — chỉ là một liên kết đến tệp giống file trước đó mà nó đã lưu trữ. Git nghĩ về dữ liệu của nó giống như dưới đây:

<p align="center">
	<img src="./img/git-hd2png.png" alt="git-hd2">
</p>

Đây là điểm khác biệt quan trọng giữa Git và gần như tất cả các VCS khác. Nó khiến Git phải xem xét lại hầu hết mọi khía cạnh của kiểm soát phiên bản mà hầu hết các hệ thống khác đã sao chép từ thế hệ trước. Điều này làm cho Git giống như một hệ thống tệp nhỏ với một số công cụ cực kỳ mạnh mẽ được xây dựng trên nó, thay vì chỉ đơn giản là một VCS.

## Dữ liệu lưu trữ trong Git đảm bảo tính toàn vẹn

Mọi thứ trước khi được lưu trữ vào Git đều đước kiểm tra bởi mã băm (hash, checksum), có nghĩa là không thể thay đổi nội dung của file mà Git không biết về sự thay đổi đó. Chức năng này giúp cho bạn không thể mất thông tin khi trao đổi dữ liệu hay file lỗi mà không thể nhận ra được. Git sử dũng mã hash SHA-1, mỗi chuỗi hash SHA-1 sinh ra căn cứ theo nội dung của file dài 40 ký tự (tạo ra từ các ký tự trong khoảng thập lục phân : 0-9, a-f) có dạng:

```hash
62FC2DBFB0CB299DD8548286FE1BB1D2B2041379
```

Mã hash kiểu này bạn sẽ gặp thường xuyên khi làm việc với Git vì mọi thứ lưu trong dữ liệu đều căn cứ theo mã hash này.

## Git có lợi ích gì?

Các dự án thực tế thường có nhiều lập trình viên làm việc song song. Vì vậy, một hệ thống kiểm soát phiên bản như Git là cần thiết để đảm bảo không có xung đột code giữa các lập trình viên.

Ngoài ra, các yêu cầu trong các dự án như vậy thay đổi thường xuyên. Vì vậy, một hệ thống kiểm soát phiên bản cho phép các nhà phát triển revert và quay lại phiên bản cũ hơn của code.

Cuối cùng, đôi khi một số dự án đang được chạy song song liên quan đến cùng một cơ sở code. Trong trường hợp như vậy, khái niệm phân nhánh trong Git là rất quan trọng.

- Dễ sử dụng, thao tác nhanh, gọn, lẹ và rất an toàn.
- Sễ dàng kết hợp các phân nhánh (branch), có thể giúp quy trình làm việc code theo nhóm đơn giản hơn rất nhiều.
- Chỉ cần clone mã nguồn từ kho chứa hoặc clone một phiên bản thay đổi nào đó từ kho chứa, hoặc một nhánh nào đó từ kho chứa là bạn có thể làm việc ở mọi lúc mọi nơi.
- Deployment sản phẩm của bạn một cách không thể nào dễ dàng hơn.

# Cài đặt và cấu hình Git

## Tải Git

Có nhiều cách để đến với trang chủ của **Git**, bạn có thể tìm kiếm trên Google và lựa chọn trong kết quả tìm kiếm hoặc đến trực tiếp trang chủ bằng cách gõ vào thanh điều hướng trình duyệt đường dẫn

> https://git-scm.com/

Bấm vào nút `Download 2.32.0 for Windows` để tải tập tin cài đặt về.

_Lưu ý rằng con số **2.32.0** là phiên bản **Git** hiện tại được phát hành, nó có thể bị thay đổi bởi các phiên bản mới hơn. Xem thêm ảnh minh họa bên dưới_

<p align="center">
	<img src="./img/Git-Homepage1.png" alt = "git-hp">
</P>

Hệ thống trang tải của Git sẽ tự động gửi tập tin cài đặt phù hợp với hệ điều hành Windows hiện tại của bạn. _Ngoài ra, bạn còn có thể tải thêm các phiên bản khác tùy ý._

<p align="center">
	<img src="./img/git-hp2.png" alt = "git-hp">
</P>

## Cài đặt Git

Sau quá trình chờ tải về, bạn sẽ có được một tệp thực thi trên máy có tên dạng `Git-2.32.02-64-bit.exe`, trong đó:

- **2.32.0** đã nói ở trên bước 1 rồi, là phiên bản của Git lúc đó.
- **64-bit** là kiến trúc mà hệ điều hành Windows của máy đang dùng để cài Git. _Xem thêm ảnh minh họa bên dưới:_

<p align="center">
	<img src="./img/package.png" alt = "git-hp">
</P>

Thực thi tập tin đó bằng cách `Bấm đôi chuột` hoặc `Bấm chuột phải` lên tệp đó rồi chọn `Open`.

Tiếp tục, chúng ta sẽ gặp `Điều khoản (Giấy phép)`, nếu đọc tốt tiếng Anh thì bạn có thể dành thời gian để đọc cho rõ. Bình thường, chúng ta hay `Đồng ý` mà không đọc gì tất.

Đọc xong rồi thì nhấn nút `Next `. _Xem thêm ảnh minh họa bên dưới:_

<p align="center">
	<img src="./img/Step1.png" alt = "step1">
</P>

Chương trình cài đặt sẽ cho chúng ta lựa chọn **vị trí lưu trữ để cài đặt chương trình Git**. Bạn có thể nhấn nút `Browse`... để chọn lại hoặc gõ đường dẫn vào ô. Đồng thời, chương trình cài đặt cũng sẽ cho bạn biết mức độ chiếm dụng của dữ liệu sẽ cài lên máy được yêu cầu để chứa là bao nhiêu (kích cỡ MB tối thiểu). Chọn xong đường dẫn rồi thì nhấn `Next`.

Trình cài đặt lại cho bạn một danh sách các lựa chọn:

**Các lựa chọn đã được chọn sẵn (tick)**: Bao gồm các trình cơ bản của Git là dòng lệnh, giao diện đồ họa, các gói hỗ trợ, khai báo loại tập tin,... Chúng ta nên để cho nó chọn đi.

Nói thêm về các dòng chưa chọn:

- **Additional icon, bao gồm On the Desktop**: là cài biểu tượng lên màn hình làm việc để bạn mở giao diện đồ họa và cửa sổ dòng lệnh của Git nhanh hơn. Cũng nên chọn chứ! Nếu bạn lười vào Start menu.
- **Use a TrueType font in all console windows**: là dùng Phông chữ kiểu TrueType cho tất cả các cửa sổ dòng lệnh. Nếu chọn dòng này, Git có thể hỗ trợ tốt hơn tiếng Việt trên các cửa sổ lệnh, bạn dùng giao diện đồ họa thì không cần chọn cũng được.
- **Check daily for Git for Windows updates**: là kiểm tra phiên bản hằng ngày xem có Git mới không để cập nhật luôn. Nếu bạn là người thích sự ổn định, ít thay đổi thì có thể bỏ qua lựa chọn này, còn nếu bạn là người thích theo đuổi những điều mới mẽ thì chọn để xem các tính năng của Git mới sau này là gì nhé! Ngoài ra, cập nhật thường xuyên cũng là một trong những việc tăng cường bảo mật, khắc phục các lỗi của bản cũ.
  Chọn xong sau đó nhấn `Next`
- **Add a git Bash profile to Windows Terminal**: Thêm shell git Bash vào Windows Terminal. Đây là tính năng khá mới và thích hợp cho Windows 11.

_Xem thêm ảnh minh họa bên dưới:_

<p align="center">
	<img src="./img/Step3.png" alt = "step1">
</P>

Quá trời nhiều lựa chọn, và tiếp theo là lựa chọn xem nên đạt Git vào Start menu như thế nào. Có thể chọn `Don't create a Start Menu folder` để không tạo ra cái thư mục Git trên Start Menu, nếu bạn không cần dùng tới. Bình thường, cứ không chọn, để nguyên như vậy rồi bấm `Next` thôi.

Sau khi lựa chọn Start Menu, trình cài đặt yêu cầu lựa chọn một chương trình soạn thảo để chúng ta có thể biên tập lệnh cho Git bash. Mặc đinh là dùng Vim. Xem hình ảnh minh họa bên dưới. Tuy nhiên tôi sẽ sử dụng Visual Studio Code vì máy tính Windows của mình đã có cài sẵn rồi.

<p align="center">
	<img src="./img/Step4.png" alt = "step1">
</P>

Tiếp đên, trình cài đặt sẽ hỏi chúng ta lựa chọn tên nhanh sau khi gõ lệnh `git init`, Ở phần này mình sẽ để mặc định là sau khi gõ lệnh `git init` sẽ tạo nhánh có tên là `master`

<p align="center">
	<img src="./img/Step5.png" alt = "step1">
</P>

Tiếp theo, trình cài đặt Git yêu cầu chúng ta lựa chọn cài đặt về biến môi trường, nếu không cần dùng biến `PATH` để là môi trường mặc định cho Git thì bạn có thể lựa chọn `Use Git from Git Bash only`.

Mình cài Git trên Windows, cũng nên tạo một môi trường cho Git để thuận tiện hơn. Vì thế mình vẫn để nguyên lựa chọn là `Git from the command line and also from 3rd-party software`. Rồi còn chờ gì nữa mà không nhấn `Next`. Xem hình ảnh minh họa bên dưới.

<p align="center">
	<img src="./img/Step6.png" alt = "step1">
</P>

Bên dưới, là hình ảnh trình cài đặt Git yêu cầu bạn lựa chọn sử dụng phương thức bảo mật nào cho các kết nối giao thức HTTPS (giap thức web tăng cường bảo mật). Bạn có thể chọn dùng theo loại chứng chỉ nào mà bạn thích. Ở đây, tôi vẫn sẽ để mặc định là `Use the OpenSSL library` để sử dụng thư viện chứng chỉ bảo mật này (thư viện mở).

Nhấn tiếp nút `Next`.

<p align="center">
	<img src="./img/Step7.png" alt = "step1">
</P>

Tiếp theo, lựa chọn chế độ dấu kết thúc dòng (xuống dòng). Sở dĩ có lựa chọn này là do dấu xuống dòng trong hệ điều hành Linux, Unix, MacOS và Windows là khác nhau.

Chúng ta cứ để mặc định là `Checkout Windows-style, commit Unix-style line endings` để Git tự chuyển qua lại giữa các loại này khi tải mã nguồn lên xuống giữa máy Windows của mình và máy chủ lưu trữ Repository. Xem hình ảnh minh họa bên dưới

Rồi, bấm tiếp nút `Next`.

<p align="center">
	<img src="./img/Step8.png" alt = "step1">
</P>

Tiếp theo trình cài đặt Git yêu cầu chúng ta lựa chọn chương trình hiển thị cửa sổ dòng lệnh để tương tác với chúng ta về sau.

Bạn nào là Fan ruột thật sự ruột của Windows thì chọn `Use Windows' default console window` để chọn cái màn hình đen chữ trắng mặc định của Windows (mách nhỏ là nó có thể đổi màu).

Tuy nhiên, để cho thuận tiện hiển thị tiếng Việt và đẹp mắt, chúng ta nên chọn như mặc định là Use `MinTTY (the default terminal of MSYS2)` để Git cài một trình giả lập cửa sổ dòng lệnh tên là `MinTTY` của `MSYS2`. Bấm nút `Next` tiếp thôi nào!

<p align="center">
	<img src="./img/Step9.png" alt = "step1">
</P>

Tiếp theo, trình cài đặt Git sẽ hỏi thiết lập `git pull`, ở mình sẽ để `Default` và ấn `Next`.

<p align="center">
	<img src="./img/Step10.png" alt = "step1">
</P>

Tiếp theo git sẽ hỏi chọn khả năng trợ giúp khi sử dụng Git, nếu như bạn không muốn trợ giúp thì hãy ấn `None`. Rồi ân `Next`

<p align="center">
	<img src="./img/Step11.png" alt = "step1">
</P>

Tiếp theo là một số cài đặt về lưu trữ (cài đặt mở rộng). Cứ mặc định mà bấm `Next` thôi bạn ơi! Xem hình ảnh minh họa bên dưới.

<p align="center">
	<img src="./img/Step12.png" alt = "step1">
</P>

Tiếp theo là một số cài đặt về thử ngiệm. Sau đó ấn `Install` để cài đặt. Xem hình ảnh minh họa bên dưới.

<p align="center">
	<img src="./img/Step13.png" alt = "step1">
</P>

Sau khi cài đặt xong mở PowerShell hoặc Command Prompt lên gõ lệnh:

```powershell
git --version
```

Nếu kết quả trả về như hình bên dưới là bạn đã cài đặt Git thành công.

<p align="center">
	<img src="./img/Step14.png" alt = "step1">
</P>

Vậy là chúng ta đã cài đặt xong Git!!

## Cài đặt Git trên MacOS và Ubuntu

**MacOS**

**Bước 1:** cài đặt Git

Mở terminal và chạy lệnh dưới đây để cài đặt Git bằng Homebrew:

```bash
brew install git
```

Lệnh trên sẽ cài đặt Git trên máy của chúng ta. Bước tiếp theo là xác minh cài đặt.

**Bước 2:** Xác minh cài đặt

Điều cần thiết là phải đảm bảo rằng quá trình cài đặt có thành công hay không.

Để xác minh xem cài đặt đã thành công hay chưa, hãy chạy lệnh dưới đây:

```bash
git --version
```

Lệnh trên sẽ hiển thị phiên bản đã được cài đặt trên hệ thống của bạn. Hãy xem xét đầu ra dưới đây:

```bash
git version 2.32.0
```

**Ubuntu**

**Bước 1:** cài đặt Git

Mở terminal và chạy lệnh dưới đây để cài đặt Git:

```bash
sudo apt install git all
```

Lệnh trên sẽ cài đặt Git trên máy của chúng ta. Bước tiếp theo là xác minh cài đặt.

**Bước 2:** Xác minh cài đặt

Điều cần thiết là phải đảm bảo rằng quá trình cài đặt có thành công hay không.

Để xác minh xem cài đặt đã thành công hay chưa, hãy chạy lệnh dưới đây:

```bash
git --version
```

Lệnh trên sẽ hiển thị phiên bản đã được cài đặt trên hệ thống của bạn. Hãy xem xét đầu ra dưới đây:

```bash
git version 2.32.0
```

# Trạng thái của Git

Mỗi tập tin trong Git được quản lý dựa trên ba trạng thái đó là **committed**, **modified**, và **staged**. Trong đó:

- **Committed** có nghĩa là dữ liệu đã được lưu trữ một cách an toàn trong cơ sở dữ liệu, tức là những gì bạn đã commit thành công.
- **Staged** là bạn đã đánh dấu sẽ commit phiên bản hiện tại của một tập tin đã chỉnh sửa trong lần commit sắp tới. Trạng thái này xảy ra khi bạn sử dụng lệnh git add <file_name> nhưng chưa commit.
- **Modified** có nghĩa là bạn đã thay đổi tập tin nhưng chưa commit vào cơ sở dữ liệu, tức là bạn chưa sử dụng lênh git add và git commit.

Như vậy với 3 trạng thái này đã tạo ra ba phần riêng biệt của một dự án có sử dụng Git:

- **Khu vực Git (Git directory)**: Là thư mục lưu trữ siêu dữ liệu (metadata) và cơ sở dữ liệu của dự án, thư mục này sẽ bị ẩn bởi hệ điều hành Windows nên bạn phải bật chức năng hiển thị file ẩn thì mới thấy được. Khu vực này sẽ tiếp nhận và lưu trữ các commit từ stage area.
- **Khu vực làm việc (Working directory)**: Nếu bạn không sử dụng Remote repository thì đây là bản sao của dự án, còn không thì đây là thư muc chính của dự án và branch master chính là bản chính, còn các branch mới tạo là branch bản sao.
- **Khu vực tổ chức (staging area)**: đây là một tập tin đơn giản nằm trong thư mục git, nó sẽ chứa thông tin về trạng thái của một file trong dự án.

<p align="center">
	<img src="./img/WW.png" alt = "step1">
</P>

Như vậy nếu bạn thay đổi một file nhưng chưa sử dụng lệnh git add và git commit thì file đó ở trạng thái Modified, còn nếu bạn đã sử dụng lệnh git add thì sẽ ở trạng thái staged, còn đã commit thì sẽ ở trạng thái Committed.

**Commited - sửa + add + commit**

```bash
$ git checkout task1
$ git add demo.txt
$ git commit -m "Sua file demo.txt"
```

**Staged - Sửa + add**

```bash
$ git checkout task1
$ git add demo.txt
```

**Modified - Sửa + ko làm gì**

```bash
$ git checkout task1
```

# Lệnh cơ bản
