# Problem Hypothesis Brief — AI Support Radar

**Case:** C — AI Support Radar (VLearn) · **Lab 17, Chặng 1** · **Ngày:** 17/08/2026
**Trạng thái:** `HYPOTHESIS` — chưa có evidence từ user. Không mục nào dưới đây được coi là fact cho tới khi Chặng 2 kiểm chứng.

> Toàn bộ brief này là **suy luận từ solution directive**, không phải phát hiện từ người dùng. Mục đích của nó không phải là đúng, mà là **đủ cụ thể để một cuộc phỏng vấn có thể làm nó sai**.

---

## 1. Solution — Gỡ solution khỏi hình thức cụ thể

### Directive nguyên văn

> Sau mỗi phiên học, hệ thống phân tích các tín hiệu như di chuyển giữa slide, dừng lâu hoặc xem lại, highlight và ghi chú, đánh dấu "Chưa hiểu", thay đổi câu trả lời, và nội dung trao đổi với AI Chat. AI tạo một **Support Queue** cho giảng viên, gồm: (1) những học viên có thể cần hỗ trợ, (2) phần nội dung họ có thể đang gặp khó khăn, (3) các tín hiệu dẫn đến nhận định đó, (4) một hành động hỗ trợ được đề xuất. Giảng viên xem lại và quyết định có liên hệ với học viên hay không.

| Thành phần | Directive đã mô tả |
| --- | --- |
| Trigger | Kết thúc một phiên học |
| Input | Slide navigation, notes, answers, AI Chat |
| AI action | Suy đoán nhu cầu hỗ trợ và xếp mức ưu tiên |
| Output | Support Queue cho giảng viên |
| Human control | Giảng viên quyết định có can thiệp hay không |

### Phần nào của directive là hình thức, không phải nhu cầu

| Trong directive | Thực chất là |
| --- | --- |
| "Support Queue" | Tên màn hình / feature |
| "xếp mức ưu tiên" | Cơ chế thuật toán |
| "AI phân tích tín hiệu" | Lựa chọn công nghệ |
| "Sau mỗi phiên học" | Nhịp do hệ thống chọn — chưa chắc là nhịp làm việc của người dùng |
| "4 mục trong queue" | Định dạng trình bày |

Bỏ hết những thứ trên, phần còn lại là:

### Capability trung tính

> **Rút ngắn khoảng thời gian từ lúc một học viên bắt đầu mắc kẹt đến lúc có người biết và can thiệp — mà không đòi hỏi học viên phải tự lên tiếng.**

**Kiểm tra:** capability này có thể được tạo ra bằng nhiều cách không dùng AI — TA ngồi trong phiên và quan sát, một quiz chốt 3 câu cuối buổi, một nút "tôi đang kẹt" hiển thị cho instructor, hoặc một cuộc gọi 5 phút cuối tuần. Việc directive chọn cách "AI đọc tín hiệu hành vi" là **một lựa chọn triển khai, không phải điều kiện bắt buộc**. Ghi lại điều này để không mặc định cách được giao là cách duy nhất.

---

## 2. Change — Chuỗi thay đổi được kỳ vọng

```
Solution → Instructor mở và đọc queue → Instructor tin đủ để hành động
        → Instructor liên hệ đúng người, đúng lúc → Learner nhận hỗ trợ và quay lại học
        → Outcome
```

### Các thay đổi được kỳ vọng

| # | Thay đổi | Ai phải đổi | Output hay Outcome | Điều kiện ngầm chưa được nói ra |
| --- | --- | --- | --- | --- |
| 1 | Chuyển từ phát hiện bị động (chờ học viên hỏi, chờ điểm kém) sang rà một danh sách chủ động sau mỗi phiên | Instructor | Behavior change | Instructor có thời gian và thói quen làm việc sau mỗi phiên |
| 2 | Học viên đang im lặng được tiếp cận **trước khi** họ tự bỏ cuộc | Learner (phản ứng) | Outcome — chỉ ảnh hưởng được | Learner chấp nhận bị tiếp cận, và việc tiếp cận thực sự giúp được |
| 3 | Tỷ lệ hoàn thành / kết quả học tăng | Cả hệ thống | Outcome xa nhất | Có rất nhiều yếu tố khác chi phối; không quy trực tiếp về feature được |

### Output vs Outcome

- **Output team tạo ra:** Support Queue được sinh đúng hạn, với tín hiệu đủ tin cậy.
- **Outcome team chỉ ảnh hưởng được:** learner được gỡ kẹt và học tiếp.

Giữa hai thứ này có **ít nhất hai hành vi con người** phải xảy ra: instructor mở queue *và* hành động; learner phản hồi *và* thấy hữu ích.

### Điểm gãy lớn nhất

**Nếu instructor không đổi hành vi, solution tạo ra 0 outcome.** Queue vẫn được sinh ra hoàn hảo mỗi ngày và không ai được giúp. Đây là lý do chọn actor ở mục 3.

---

## 3. Actor — Các nhóm người liên quan

| Actor | Họ đang làm gì | Pain hoặc hậu quả có thể có | Họ hưởng lợi thế nào |
| --- | --- | --- | --- |
| **Learner** | Học phiên, tự xoay xở khi mơ hồ | Kẹt âm thầm, trôi dần, mất động lực, bỏ khóa | Được gỡ kẹt sớm — *nếu* họ muốn bị tiếp cận |
| **Instructor** | Dạy, chấm, trả lời câu hỏi được hỏi ra | Chỉ thấy được người chủ động; phát hiện muộn khi đã quá xa | Biết sớm hơn ai cần kèm |
| **Coach / TA** | Hỗ trợ 1-1 theo yêu cầu | Không biết bắt đầu từ ai; bị phân bổ theo cảm tính | Có danh sách ưu tiên để phân bổ giờ kèm |
| **Program manager** | Theo dõi completion rate của khóa | Learner rơi rụng, chỉ biết qua báo cáo cuối kỳ | Hưởng lợi gián tiếp — **không điều tra vòng này** |

### Actor nhóm chọn điều tra trước: **Instructor / Coach**

**Vì sao chọn nhánh này thay vì learner:**

1. Họ là **mắt xích gãy** của chuỗi Change ở mục 2 — người duy nhất phải đổi hành vi để bất cứ outcome nào xảy ra.
2. Nếu job "biết ai cần giúp sau mỗi phiên" **không tồn tại**, hoặc đã được giải quyết đủ tốt bằng cách khác, thì toàn bộ solution vô nghĩa — kể cả khi learner có pain thật.
3. Learner pain có thể có thật mà solution vẫn thất bại. Instructor job không tồn tại thì solution *chắc chắn* thất bại. Đây là giả thuyết rẻ nhất để bác bỏ.

**Learner vẫn được phỏng vấn**, nhưng với vai trò khác: kiểm tra **tiền đề** của giả thuyết instructor — "học viên kẹt có thực sự im lặng không?" và "họ có muốn bị tiếp cận không?". Xem mục 6.

---

## 4. Situation & Job

### Khoảnh khắc được chọn

Ngay sau khi một phiên học kết thúc và lớp giải tán — trước buổi kế tiếp.

```
Tình huống bắt đầu   → Phiên học vừa kết thúc, instructor không còn nhìn thấy lớp
→ User muốn hoàn thành → Xác định ai cần kèm thêm trước buổi sau
→ Hiện tại họ làm      → Nhớ lại ai đã hỏi, lướt điểm quiz, nhắn vài người quen mặt
→ Điểm gặp vướng mắc   → Những người im lặng không để lại tín hiệu nào để nhớ lại
```

### Mô tả Situation & Job

> Khi **một phiên học vừa kết thúc và lớp đã giải tán**, **instructor** đang cố **xác định ai trong lớp cần được kèm thêm trước buổi sau** bằng cách **nhớ lại ai đã đặt câu hỏi, lướt qua điểm bài tập, và nhắn hỏi vài học viên họ quen mặt**.

### JTBD Hypothesis — Instructor (chính)

> Khi **một phiên học vừa kết thúc và tôi không còn nhìn thấy lớp nữa**, tôi muốn **biết ai đang thực sự mắc kẹt**, để có thể **can thiệp trước khi họ tụt lại quá xa hoặc bỏ cuộc**.

### JTBD Hypothesis — Learner (phụ, dùng để đối chiếu)

> Khi **tôi học xong một phiên mà vẫn thấy mơ hồ ở một phần nội dung**, tôi muốn **giải quyết chỗ mơ hồ đó trước buổi sau**, để **không bị trôi theo phần tiếp theo**.

**Kiểm tra "job tồn tại khi bỏ AI và feature":** ✅ Đạt. Instructor lớp offline làm chính xác việc này bằng cách đi quanh lớp và nhìn nét mặt. Job có trước sản phẩm.

---

## 5. Pain — Các cách giải thích cạnh tranh

### Pain Hypothesis A — Vấn đề **phát hiện**

> Khi **một phiên học vừa kết thúc**, **instructor** gặp khó khăn trong việc **xác định ai đang mắc kẹt** vì **tín hiệu duy nhất họ có là những người chủ động hỏi và điểm bài nộp — trong khi những học viên khó khăn nhất thường im lặng**, dẫn đến **chỉ phát hiện khi học viên đã trượt bài kiểm tra hoặc ngừng vào lớp, lúc đó can thiệp đã quá muộn**.

### Pain Hypothesis B — Vấn đề **năng lực & quy trình** (cách giải thích cạnh tranh)

> Khi **một phiên học vừa kết thúc**, **instructor** gặp khó khăn trong việc **hỗ trợ học viên mắc kẹt** vì **họ đã biết khá rõ ai đang đuối (qua điểm, qua việc không nộp bài) nhưng không có thời gian, không có kênh liên hệ tiện, và việc kèm 1-1 không được tính vào khối lượng công việc**, dẫn đến **bỏ qua cả những trường hợp đã nhìn thấy rõ ràng**.

### Pain Hypothesis C — Khác actor (learner-side, giữ để đối chiếu)

> Khi **thấy mơ hồ sau một phiên học**, **learner** gặp khó khăn trong việc **xin giúp đỡ** vì **ngại lộ ra mình không theo kịp và không biết hỏi ai hay hỏi câu gì cho đúng**, dẫn đến **tự tra Google, hỏi bạn cùng lớp, hoặc bỏ qua và hy vọng phần sau sẽ dễ hơn**.

### A và B khác nhau ở đâu — và vì sao điều đó quan trọng

| | Nếu **A** đúng | Nếu **B** đúng |
| --- | --- | --- |
| Bản chất vấn đề | Thiếu tín hiệu | Thiếu thời gian & động lực |
| Support Queue làm gì | Cung cấp thứ instructor chưa có → có giá trị | Trình bày lại thứ họ đã biết → **thêm việc, không thêm giá trị** |
| Hướng giải quyết đúng | Tăng khả năng quan sát | Giảm chi phí hành động: template tin nhắn, phân việc cho TA, tính giờ kèm vào KPI |

### Giả thuyết nhóm chọn điều tra trước: **A**

**Lý do chọn:** A chính là giả thuyết mà solution directive đang **ngầm giả định nhưng chưa nói ra**. Nếu A sai và B đúng, Support Queue không tạo ra thay đổi nào — nó chỉ hiển thị lại thông tin instructor đã có, và team sẽ xây đúng thứ được giao nhưng sai loại vấn đề. Đây là giả thuyết rẻ nhất để bác bỏ và tốn kém nhất nếu bỏ qua.

**Câu hỏi phân biệt A/B trong phỏng vấn:**
> "Lần gần nhất anh/chị phát hiện một học viên đang mắc kẹt — anh/chị biết bằng cách nào, và sau đó đã làm gì?"

- Kể được **cách phát hiện** rõ ràng nhưng **không kể được hành động** → nghiêng về **B**.
- Chỉ phát hiện **muộn hoặc tình cờ** → nghiêng về **A**.

---

## 6. Evidence — Điều cần tìm trước khi viết câu hỏi

Nguyên tắc: chỉ nhận **sự kiện đã xảy ra**. Một problem statement nghe hợp lý không phải evidence; một ý kiến về tương lai càng không.

| # | Điều cần tìm | Câu hỏi kể chuyện | Tính là evidence khi | **Không** tính là evidence |
| --- | --- | --- | --- | --- |
| 1 | Recency & tần suất | "Lần gần nhất chuyện đó xảy ra là khi nào?" | Kể được một buổi cụ thể, gần đây | "Chuyện đó xảy ra suốt" (không có sự kiện) |
| 2 | Cách phát hiện hiện tại | "Lúc đó anh/chị biết bằng cách nào?" | Nêu được nguồn tín hiệu cụ thể | "Nhìn qua thì biết thôi" |
| 3 | Workaround & công sức | "Sau đó anh/chị làm gì? Mất bao lâu?" | Có công cụ tự chế: file Excel theo dõi, nhóm chat riêng, danh sách tay | "Cũng nên làm gì đó" |
| 4 | Hậu quả quan sát được | "Kết quả của lần đó ra sao?" | Có tên người, có con số: bỏ khóa, học lại, trượt | "Chắc là ảnh hưởng chất lượng" |
| 5 | Chi phí của việc **không** hành động | "Có lần nào anh/chị biết mà không làm gì không? Vì sao?" | Câu trả lời trung thực → **phân biệt A và B** | Câu trả lời phòng thủ |
| 6 | Learner có muốn bị tiếp cận không | "Đã bao giờ có ai chủ động nhắn hỏi khi bạn chưa lên tiếng chưa? Lúc đó bạn thấy thế nào?" | Kể được phản ứng thật, kể cả phản ứng khó chịu | "Chắc là thấy được quan tâm" |

### Kill criteria — evidence sẽ khiến nhóm sửa hoặc bác bỏ hypothesis

- ❌ **Instructor mô tả được một cách phát hiện đang dùng, đủ nhanh và đáng tin** → A yếu, chuyển trọng tâm sang B.
- ❌ **Instructor thừa nhận biết mà không liên hệ vì hết thời gian** → A sai, B đúng, solution sai loại vấn đề.
- ❌ **Không instructor nào có workaround nào cả** (không file theo dõi, không nhắn riêng) → pain có thể tồn tại nhưng **không đủ đau để hành động** — solution sẽ không được dùng.
- ❌ **Learner phản ứng tiêu cực với việc bị tiếp cận dựa trên hành vi bị theo dõi** → xuất hiện risk mới (giám sát / riêng tư), chuỗi Change gãy ở mắt xích cuối.
- ❌ **Learner kể rằng khi kẹt họ đã hỏi bạn / AI Chat / Google và giải quyết được** → pain đã có workaround đủ tốt, C yếu, giá trị của toàn case giảm.

### Phân bổ phỏng vấn

| Slot | Người | Mục tiêu chính |
| --- | --- | --- |
| 1 | Instructor hoặc Coach | Job có tồn tại không; phân biệt **A vs B** |
| 2 | Learner | Tiền đề của A: khi kẹt thì im lặng hay lên tiếng? |
| 3 | Learner | Mắt xích cuối: phản ứng thật với việc bị chủ động tiếp cận |

> **Ghi chú giới hạn — bắt buộc ghi vào báo cáo nếu không có coach/instructor trong giờ lab:**
> *"Vòng này chỉ có learner-side evidence; instructor-side job chưa được kiểm chứng."*
> **Hệ quả:** không thể phân biệt A và B trong vòng này. Brief phải giữ nguyên trạng thái chưa kết luận, và không được dùng learner evidence để suy ra instructor job.

---

## 7. Assumption log — Những bước nhảy niềm tin

| # | Giả định | Thuộc lớp | Rủi ro nếu sai | Có kế hoạch kiểm chứng? |
| --- | --- | --- | --- | --- |
| 1 | Học viên gặp khó khăn thường **im lặng** thay vì hỏi | Pain | Nếu sai, tín hiệu đã sẵn có → không cần radar | ✅ Slot 2 |
| 2 | Tín hiệu hành vi (dừng lâu, xem lại slide) **tương quan** với "không hiểu" | Input / Solution | Dừng lâu có thể là ghi chép kỹ, hoặc đi pha cà phê. Queue đầy false positive → instructor mất niềm tin sau 2 tuần và ngừng mở | ⚠️ **Chưa** — cần đối chiếu log dữ liệu, ngoài phạm vi phỏng vấn |
| 3 | Instructor có thời gian đọc queue **sau mỗi phiên** | Change / Situation | Nhịp sản phẩm lệch nhịp làm việc → queue tồn đọng | ✅ Slot 1 |
| 4 | Instructor có kênh và thẩm quyền để liên hệ learner | Change | Không có thẩm quyền → không hành động được dù muốn | ✅ Slot 1 |
| 5 | Learner **chấp nhận** bị tiếp cận dựa trên hành vi được phân tích | Change / Ethics | Cảm giác bị giám sát → learner né tín hiệu, dữ liệu tự hỏng | ✅ Slot 3 |
| 6 | "Hành động hỗ trợ được đề xuất" của AI đủ dùng để instructor làm theo | Solution | Gợi ý chung chung → instructor vẫn phải tự nghĩ → không tiết kiệm gì | ⚠️ Chưa — để Chặng sau |

Giả định **#2** là rủi ro kỹ thuật lớn nhất và **không kiểm chứng được bằng phỏng vấn**. Ghi nhận rõ để không nhầm là đã được cover.

---

## 8. Trạng thái brief

| Lớp | Trạng thái |
| --- | --- |
| Solution → capability trung tính | ✅ Xong |
| Change chain & điểm gãy | ✅ Xong |
| Actor & nhánh điều tra | ✅ Xong — chọn Instructor/Coach |
| Situation & Job | ✅ Xong — có JTBD phụ cho learner |
| Pain A / B / C | ✅ Xong — chọn A, có câu hỏi phân biệt |
| Evidence plan & kill criteria | ✅ Xong |
| **Evidence thực tế từ user** | ⬜ **Chưa có — Chặng 2** |

**Điều nhóm cố tình chưa quyết:** chưa chọn giữa A và B. Việc chọn A chỉ là chọn *thứ tự điều tra*, không phải chọn kết luận. Nếu Chặng 2 nghiêng về B, brief này được viết lại chứ không được vá.
