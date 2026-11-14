$Repo = "$HOME\Rookie-Origins"
Set-Location $Repo

# 1. Put the images in an assets folder
New-Item -ItemType Directory -Force assets | Out-Null
Copy-Item "<img width="1055" height="330" alt="5195044196606670032" src="https://github.com/user-attachments/assets/3b7c08e2-53f0-46f3-a126-9aece05880b8" />
"  "assets\banner.png"
Copy-Item "<img width="994" height="785" alt="5420432668576392280" src="https://github.com/user-attachments/assets/976d411e-3fe8-46cf-8ea8-e8a47dc74fe4" />
" "assets\end.png"

# 2. Keep the existing table lines from the current README
$table = (Get-Content README.md -Encoding UTF8 | Where-Object { $_ -like "|*" }) -join "`n"

# 3. Rebuild the README
$bat    = [char]::ConvertFromUtf32(0x1F987)
$folder = [char]::ConvertFromUtf32(0x1F5C2)
$readme = @"
![Rookie Origins banner](assets/banner.png)

# $bat Rookie Origins

> *Every legend has a first night out.*

This is where I started. Not the polished work, that lives on my profile,
but the first notebooks, the first models that actually ran, and the first
time an accuracy score came back and I thought, "wait, it works?"

Some of these are messy. A few make me wince. All of them taught me
something, and I kept them here instead of hiding them.

## What's inside

Regression, classification, NLP, computer vision, recommender systems,
and a bit of math theory. Mostly classic datasets, because that's how you
learn the craft before you try to build something new.

## $folder Case Files

$table

## Why keep them?

Gotham wasn't built in a night, and neither was any of this. The gap
between these projects and what I build now is the whole point.

![The city at night](assets/end.png)
"@
[System.IO.File]::WriteAllText("$PWD\README.md", $readme, (New-Object System.Text.UTF8Encoding $false))

# 4. Push
git add -A
git commit -m "Add banner, ending image and new README text"
git push origin HEAD
