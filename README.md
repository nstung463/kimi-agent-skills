# Kimi Agent Core Skills

> Bộ core skills đầy đủ được tổng hợp từ Kimi Agent — gồm 261 skill và hơn 2.600 file workflow, reference, asset và script.

[English](#english) · [Tiếng Việt](#tiếng-việt)

## English

This repository packages the core skill library used by the Kimi Agent setup. It is organized as a reusable `skills/` collection for AI agents: each skill is a self-contained directory with a `SKILL.md` instruction file and, where needed, supporting scripts, references, assets, and templates.

The repository structure and README presentation are inspired by [thvroyal/kimi-skills](https://github.com/thvroyal/kimi-skills). The skill content in this repository comes from the local core collection at `C:\Users\Admin\Downloads\skills-kimi\skills`; it is not a fork of that reference repository.

### What is included?

| Area | Examples |
|---|---|
| Writing & content | Copywriting, SEO, email, newsletters, reports, speeches, translation, social posts |
| Research & finance | Deep research, equity and stock research, valuation, earnings, commodities, funds, risk |
| Product & planning | PRDs, campaigns, OKRs, pricing, roadmaps, sprints, Gantt plans, SaaS analysis |
| Engineering & data | Backend, API, databases, SQL, testing, Git, Kubernetes, Terraform, security, charts |
| Documents & media | DOCX, PDF, XLSX, PPTX, slides, design systems, infographics, video and podcast workflows |
| Personal & learning | ADHD support, flashcards, quizzes, tutoring, interviews, resumes, meeting and work recaps |

Important entry-point skills include:

- `docx`, `pdf`, `xlsx`, `pptx` for office documents and presentations
- `kimi-find-skills`, `kimi-skills-finder`, `kimi-help-center` for skill discovery and help
- `webapp-building`, `backend-building`, `api-doc-gen`, `database-inspector` for software work
- `deep-research`, `research-writer`, `academic-paper-reviewer` for research workflows
- `seo-audit`, `campaign-planner`, `brand-naming-lab` for marketing and content work

### Install

Install the full collection:

```bash
npx skills add nstung463/kimi-agent-skills
```

Or install/copy only the skill you need from the `skills/` directory. Every skill's `SKILL.md` documents its trigger conditions, workflow, and relevant dependencies.

### Repository layout

```text
kimi-agent-skills/
├── skills/
│   ├── docx/
│   ├── pdf/
│   ├── pptx/
│   ├── xlsx/
│   ├── kimi-find-skills/
│   └── ... 261 skill directories
├── .gitignore
└── README.md
```

### How to use a skill

1. Identify the relevant directory under `skills/`.
2. Read its `SKILL.md` before invoking the workflow.
3. Follow the skill's dependency and tool instructions.
4. Keep supporting files next to the skill when copying it to another agent environment.

## Tiếng Việt

Đây là repo chứa bộ **core skills đầy đủ của Kimi Agent**. Bộ dữ liệu được lấy từ thư mục:

```text
C:\Users\Admin\Downloads\skills-kimi\skills
```

Repo có 261 thư mục skill và hơn 2.600 file đi kèm, bao gồm hướng dẫn `SKILL.md`, script, reference, asset và template. Nội dung bao phủ nhiều nhóm: viết nội dung, nghiên cứu, tài chính, lập trình, bảo mật, dữ liệu, email, marketing, tài liệu văn phòng, slide, video, học tập và quản lý công việc.

### Cách tổ chức

Cách trình bày và cấu trúc README được học hỏi từ [thvroyal/kimi-skills](https://github.com/thvroyal/kimi-skills). Tuy nhiên, repo này **không sao chép bộ 3 skill của repo tham khảo**; toàn bộ thư mục `skills/` được viết lại theo core skills thực tế của bạn.

Mỗi skill là một thư mục độc lập. File `SKILL.md` là điểm bắt đầu để biết skill dùng khi nào, quy trình thực hiện ra sao và cần dependency nào.

### Cài đặt

```bash
npx skills add nstung463/kimi-agent-skills
```

Hoặc chỉ lấy từng thư mục cần dùng trong `skills/`, ví dụ `docx`, `pdf`, `xlsx`, `pptx`, `deep-research`, `webapp-building` hoặc `seo-audit`.

### Attribution và phạm vi

Đây là bản tổng hợp/đóng gói cộng đồng từ core skill collection của Kimi Agent. Repo này không phải sản phẩm chính thức của Kimi hoặc Moonshot AI và không đại diện cho các tác giả/đơn vị gốc. Khi sử dụng, chỉnh sửa hoặc tái phân phối, hãy giữ attribution, đọc license trong từng skill và tuân thủ quyền của tác giả tương ứng.

## Credits

- Core skill source: Kimi Agent skill collection supplied by the repository owner
- Repository organization: inspired by [thvroyal/kimi-skills](https://github.com/thvroyal/kimi-skills)

## License

License và attribution có thể khác nhau giữa các skill. Hãy xem file `LICENSE`, `LICENSE.txt` hoặc phần ghi chú trong từng thư mục skill trước khi tái phân phối hoặc dùng cho mục đích thương mại.
