# Individual Report: Lab 3 - Chatbot vs ReAct Agent

- **Student Name**: Lưu Quang Lực
- **Student ID**: 2A202600121
- **Date**: 06/04/2026

---

## I. Technical Contribution (15 Points)

- **Modules Implementated**: src/tools/get_event.py
- **Code Highlights**: Hàm get_nearby_places_serpapi
- **Documentation**: Lấy danh sách quán coffee ở gần.

---

## II. Debugging Case Study (10 Points)

*Analyze a specific failure event you encountered during the lab using the logging system.*

- **Problem Description**: `Action: get_nearby_places_serpapi không được chạy khi step dưới 3
- **Log Source**: {"timestamp": "2026-04-06T09:43:08.684974", "event": "AGENT_END", "data": {"steps": 2, "reason": "no_action"}}
- **Diagnosis**: Prompt thiếu ràng buộc bắt buộc gọi tool
- **Solution**: thêm prompt "Must call get_nearby_places_serpapi before finish.\n"

---

## III. Personal Insights: Chatbot vs ReAct (10 Points)

*Reflect on the reasoning capability difference.*

1.  **Reasoning**: Khối Thought giúp hiển thị rõ ràng quá trình suy luận trung gian, giúp debug agent dễ hơn --> đưa ra câu trả lời sát với
    yêu cầu, Hiểu mong muốn người dùng hơn. Chatbot chỉ liệt kê, đưa ra câu trả lời chung chung, giá trị mang lại
    không cụ thể cho người dùng.
2.  **Reliability**: Agent có thể chưa thực hiện action nhưng bịa ra kết quả. Câu trả lời của chatbot
    mang lại độ tin cậy cao hơn trong 1 số trường hợp dù câu trả lời giống như liệt kê.
    Agent xem lỗi tool là vấn đề nghiêm trọng --> có thể dừng lại. Chatbot bỏ qua lỗi và tiếp tục trả lời.
    Điều này khiến chatbot bền bỉ hơn, agent dễ bị bug hơn.
3.  **Observation**: 1 quán sát tốt, rõ ràng giúp định hình action tiếp theo tốt hơn. KHi quan sát không tốt
    dẫn đến action bị bỏ qua, Agent hiểu rằng đã kết thúc.

---

## IV. Future Improvements (5 Points)

*How would you scale this for a production-level AI agent system?*

- **Scalability**: Tách agent và tool services, agent luôn quét hết tool services. Điều này
  giúp việc cập nhật tool, thêm tool và được agent sử dụng ngay.
- **Safety**: Cần có rule kiểm tra action đã được gọi chưa
- **Performance**: max_step cần linh động dựa vào độ khó task, lịch sử failure để tránh lãng phí
hoặc dừng sớm

---

> [!NOTE]
> Submit this report by renaming it to `REPORT_[YOUR_NAME].md` and placing it in this folder.
