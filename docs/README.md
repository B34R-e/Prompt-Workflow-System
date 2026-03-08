# Simple Agentic Documentation Framework 🤖

Welcome to the **Agentic Documentation Framework**. This is a documentation structure designed specifically for projects that rely heavily on AI Agents (like GitHub Copilot, Cursor, Codeium, or custom LLM scripts) for pair-programming and development.
*(Kéo xuống dưới để xem bản Tiếng Việt 🇻🇳)*

Unlike traditional wikis meant for human readers, this framework serves as an **Operating System for AI Agents**. It clearly separates instructions (prompt engineering) from data (project specifications), uses a gated pipeline to prevent hallucinations, and dynamically scales based on project size.

## 🌟 Why use this framework?

1.  **Prevents Hallucinations:** Prevents the AI from making wild assumptions by forcing it to read strict localized rules and maintain a clear separation between "Assumptions" and "Unknowns".
2.  **State Management for AI:** Uses a "Living Changelog" and "Feature Tracker" instead of raw Git history, giving the AI a clean context of what is currently active without confusing it with dead-end code refactors.
3.  **Context Optimization:** Dynamically loads rules (like testing, coding conventions, or security audits) only when the project scale demands it, keeping the context window lean for smaller PoC/Spike projects.
4.  **Enforces "Definition of Ready" (DoR):** The AI cannot jump into coding without first satisfying the prerequisites defined in the early stages (Scope -> Problem -> Requirements -> Architecture).

## 📁 Folder Structure

The framework is organized into specific directories, each with a distinct role:

*   **`00_Identify/` & `01_Checklist/` & `02_Rules/`**: The "Control/Instruction" files (written in English). These are effectively complex prompts that govern how the Agent should behave, route tasks, and validate outputs.
    *   *Note on `02_Rules/extensions/`: Contains specialized rules (like strict coding conventions, testing requirements) that are dynamically loaded for MVP or Production scale projects.*
*   **`03_README/`**: Contains instructions for using this framework.
*   **`04_Prerequisites/`**: The "Output" files (written in your native language). These store the actual facts about your project (Scope, Requirements, Architecture).
*   **`05_Research/` & `06_Analyze/`**: Scratchpads for the AI to conduct deep dives before writing code.
*   **`07_Changes_history/`**: The "Living Changelog" where the AI records active modifications.
*   **`08_Features/`**: Trackers for specific functional areas (e.g., Auth, Chat, Payments).
*   **`09_Environment/`**: Onboarding instructions and setup scripts for human developers joining the project.

## 🚀 How to Get Started

To understand how to interact with the AI using this framework, please read:
👉 **[03_README/How_to_use.md](./03_README/How_to_use.md)** 

**Basic Usage Summary:**
1. Tell your AI Agent: *"Please read `docs/02_Rules/Agent_Rules.md` and act as my pair-programmer."*
2. Follow the initialization steps to generate the `04_Prerequisites` files.
3. For daily work, simply give the Agent a task. The routing engine in `Agent_Rules.md` will automatically guide it to use the correct sub-modules (Planning, Execution, Bug Triage, etc.).

## 📝 Disclaimer & References

**Disclaimer:** This framework is built upon my personal experiences, knowledge, and practical lessons learned from developing solo and team projects alongside AI Agents. It is a highly opinionated workflow and may need further tuning for your specific use cases.

**References:**
The concepts and architectural hygiene enforced by this framework were heavily inspired by the following books:
- *Code Complete (2nd Edition)* by Steve McConnell

---
---

# 🇻🇳 Khung Tài Liệu Dành Cho AI Agent (Agentic Documentation Framework)

Chào mừng bạn đến với **Agentic Documentation Framework**. Đây là một cấu trúc tài liệu được thiết kế đặc biệt cho các dự án phụ thuộc nhiều vào AI Agents (như GitHub Copilot, Cursor, Codeium, hay các LLM script tự viết) để lập trình cặp (pair-programming).

Khác với các dạng Wiki truyền thống dành cho người đọc, framework này đóng vai trò như một **"Hệ Điều Hành" dành cho AI Agents**. Nó phân định rõ ràng giữa Hướng dẫn/Prompt và Dữ liệu/Nội dung dự án, sử dụng một quy trình có cổng chặn (gated pipeline) để chống ảo giác, đồng thời tự động co giãn linh hoạt theo quy mô dự án.

## 🌟 Tại sao nên dùng framework này?

1.  **Chống Ảo Giác (Prevents Hallucinations):** Ngăn AI tự đưa ra các giả định hoang đường bằng cách ép buộc nó đọc các bộ nguyên tắc cục bộ cực kỳ nghiêm ngặt, rạch ròi giữa "Assumption" (Giả định) và "Unknown" (Chưa rõ).
2.  **Quản Lý Trạng Thái Cho AI (State Management):** Sử dụng "Living Changelog" và "Feature Tracker" thay vì Git history thô. Điều này giúp AI có bức tranh về ngữ cảnh hiện tại một cách gọn gàng, không bị nhiễu bởi các "ngõ cụt" (dead-ends) khi refactor code.
3.  **Tối Ưu Hóa Ngữ Cảnh (Context Optimization):** Tự động nạp các bộ rule (như viết test, coding convention, hay audit bảo mật) CHỈ KHI quy mô dự án yêu cầu, giúp bảo toàn dung lượng Context Window cho các dự án PoC/Spike nhỏ gọn.
4.  **Ép Buộc Chuẩn Mực (Definition of Ready - DoR):** AI không thể nhảy ngay vào việc viết code nếu chưa thỏa mãn các điều kiện tiên quyết (Prerequisites) được định nghĩa ở các bước đầu (Phạm vi dự án -> Vấn đề -> Yêu cầu hệ thống -> Kiến trúc).

## 📁 Cấu Trúc Thư Mục

Khung tài liệu được tổ chức thành các thư mục với vai trò riêng biệt rạch ròi:

*   **`00_Identify/` & `01_Checklist/` & `02_Rules/`**: Các file "Điều hướng/Chỉ thị" (Control/Instruction) – được viết bằng tiếng Anh. Đây thực chất là các prompt phức tạp để quản lý hành vi của Agent, định tuyến tác vụ và đánh giá kết quả đầu ra.
    *   *Lưu ý về thư mục `02_Rules/extensions/`: Chứa các bộ rule chuyên sâu (như chuẩn viết code, quy định test) được AI tự động nạp linh hoạt riêng cho các dự án quy mô MVP hoặc Production.*
*   **`03_README/`**: Chứa hướng dẫn sử dụng thư mục tài liệu này.
*   **`04_Prerequisites/`**: Các file "Đầu ra dự án" (Output) – được viết bằng Tiếng Việt (hoặc ngôn ngữ mẹ đẻ). Đây là nơi lưu trữ các sự thật về dự án (Phạm vi, Yêu cầu, Kiến trúc).
*   **`05_Research/` & `06_Analyze/`**: Là nơi chắp bút (scratchpads) để AI thực hiện các nghiên cứu/phân tích sâu trước khi tiến hành code.
*   **`07_Changes_history/`**: "Living Changelog" - Nơi AI ghi lại lịch sử các biến đổi mã nguồn đang active.
*   **`08_Features/`**: Các tracker theo dõi trạng thái của các nhóm tính năng (ví dụ: Auth, Chat, Payments).
*   **`09_Environment/`**: Hướng dẫn Onboarding và setup sơ khởi dành cho các lập trình viên "nửa kia" (con người) khi cấu hình dự án.

## 🚀 Hướng Dẫn Bắt Đầu

Để hiểu cách tương tác với AI khi sử dụng framework này, vui lòng đọc:
👉 **[03_README/How_to_use.md](./03_README/How_to_use.md)** 

**Tóm Tắt Cách Dùng Nhanh:**
1. Hãy ra lệnh cho AI Agent của bạn: *"Please read `docs/02_Rules/Agent_Rules.md` and act as my pair-programmer."*
2. Làm theo các bước khởi tạo (initialization) để cùng AI sinh ra các file `04_Prerequisites`.
3. Trong công việc hàng ngày, bạn chỉ việc giao task bình thường. AI engine trong `Agent_Rules.md` sẽ tự động định tuyến để sử dụng đúng các sub-modules (Planning, Execution, Bug Triage, v.v.).

## 📝 Lời Từ Chối Trách Nhiệm (Disclaimer) & Tài Liệu Tham Khảo

**Disclaimer:** Framework này được xây dựng hoàn toàn đúc kết từ những trải nghiệm, kiến thức, và học hỏi cá nhân trong quá trình phát triển các dự án thực tế (cả làm hỏa tốc solo lẫn làm việc với team) khi có sử dụng AI Agents. Đây là một workflow mang nặng tính cá nhân hóa (highly opinionated) và bạn có thể cần điều chỉnh đôi chút cho phù hợp với dự án cụ thể của mình.

**Tài Liệu Tham Khảo:**
Các nguyên lý kiến trúc và tư duy kiểm soát chất lượng phần mềm trong framework này được truyền cảm hứng to lớn từ tựa sách nổi tiếng:
- *Code Complete (2nd Edition)* - Tác giả: Steve McConnell
