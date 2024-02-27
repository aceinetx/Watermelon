# Known issues:
- Closing ImGui Window can sometimes lead to exit code not being 0
- You can only break loops at the end of it (otherwise it would not skip to loop end but continue for 1 cycle)
