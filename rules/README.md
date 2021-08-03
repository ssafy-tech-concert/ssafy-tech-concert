# Git Rules

## 🔜 깃 커밋 순서

`git pull` > `git status` > `git add 발표내용.md` and `git add README.md` > `git commit -m "Upload : HTTP.md 파일 업로드"` > `git push`

<br />

## 📝 Git Commit Message Convention

```bash
Update : 08.01. 발표 제목 공지
Upload : 발표내용.md 파일 업로드
Revise : 수정한 내용 설명
Delete : 삭제한 파일 설명
```

<br />

## ❗ 주의사항

&nbsp;&nbsp;항시 파일을 **Staging Area**에 올리기 전에 `git status` 명령어를 통해 깃 상태를 확인하고 불필요한 파일이 있다면 `.gitignore` 파일에 추가시켜서 제외하거나 `git add 발표내용.md` 명령어를 통해 원하는 파일만 **Staging Area**로 올린 후 커밋 시켜주세요.

> 즉, 깃 상태 확인하지 않고 `git add .` 명령어로 바로 올리는 것은 조심해 주세요!
