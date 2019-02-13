# Irc Web Bot
### Basic Web API that allows http requests to send messages to an IRC server
---
This project was developed to allow CI/CD pipelines to integrate with IRC.
* Not complex
* Not necessarily secure
* Not advanced

### Build pipeline
Building is done on CircleCI using a split config that is checked that it is up to date during the pipeline process.
Kinda of "self healing", but more importantly allowed me to split all jobs and commands into their own files to make the config easier to read.
The compilation of the config is done as the first job of circle and if the compiled version is outdated then circle updates it, pushes to GH to trigger another build, and then fails the build.
This ensures that the main config is always up to date with the decomposed config.
#### The pipeline
![My build pipeline](docs/img/pipeline.png)
[Link to edit](https://mermaidjs.github.io/mermaid-live-editor/#/edit/eyJjb2RlIjoiZ3JhcGggTFJcblxudHJpZ2dlcntcIjxoMj5UcmlnZ2VyPC9oMj5cIn1cblxuY2hlY2tfY2lyY2xlW1wiPGgyPmNoZWNrX2NpcmNsZTwvaDI-Q29tcGlsZXMgY2lyY2xlQ0kgY29uZmlnIGFuZDxici8-Y2hlY2tzIHRoYXQgaXQgaXMgdXAgdG8gZGF0ZVwiXVxuXG5ub3RpZnlfc3RhcnRbXCI8aDI-bm90aWZ5X3N0YXJ0PC9oMj5TZW5kcyBtZXNzYWdlIHRvIElSQzxici8-bm90aWZ5aW5nIG9mIGJ1aWxkIHN0YXJ0XCJdXG5cbmJ1aWxkX3NlcnZlcltcIjxoMj5idWlsZF9zZXJ2ZXI8L2gyPlJ1bnMgZ3JhZGxlIGJvb3RKYXIgdG88L2JyPmJ1aWxkIGFuZCBwYWNrYWdlIChObyB0ZXN0cylcIl1cblxudGVzdF9zZXJ2ZXJbXCI8aDI-dGVzdF9zZXJ2ZXI8L2gyPlJ1bnMgdW5pdCB0ZXN0c1wiXVxuXG5yZWxlYXNlX2FwcHJvdmFsW1wiPGgyPnJlbGVhc2VfYXBwcm92YWw8L2gyPkhvbGRzIHJlbGVhc2VzIHdhaXRpbmcgZm9yPGJyLz5tYW51YWwgYXBwcm92YWxcIl1cblxucmVxdWVzdF9hcHByb3ZhbFtcIjxoMj5yZXF1ZXN0X2FwcHJvdmFsPC9oMj5NZXNzYWdlcyBJUkMgdG8gcmVxdWVzdDwvYnI-bWFudWFsIGFwcHJvdmFsXCJdXG5cbm5vdGlmeV9zdWNjZXNzW1wiPGgyPm5vdGlmeV9zdWNjZXNzPC9oMj5NZXNzYWdlcyBJUkMgdG8gaW5mb3JtIG9mPC9icj5zdWNjZXNzZnVsIGJ1aWxkIGFuZCB0ZXN0c1wiXVxuXG5wdWJsaXNoX2dpdGh1Yl9yZWxlYXNlW1wiPGgyPnB1Ymxpc2hfZ2l0aHViX3JlbGVhc2U8L2gyPlRyaWdnZXJzIGdpdGh1YiByZWxlYXNlIGFuZCB0YWdzPGJyLz5QdWJsaXNoZXMgYXJ0aWZhY3RzIHRvIGdpdGh1YlwiXVxuXG5kb2NrZXJfcmVsZWFzZVtcIjxoMj5kb2NrZXJfcmVsZWFzZTwvaDI-QnVpbGRzIGFuZCBwdXNoZXMgbmV3PC9icj5pbWFnZSB0byBkb2NrZXIgaHViXCJdXG5cbm5vdGlmeV9yZWxlYXNlW1wiPGgyPm5vdGlmeV9yZWxlYXNlPC9oMj5NZXNzYWdlcyBJUkMgaW5mb3JtaW5nPC9icj5vZiBuZXcgcmVsZWFzZSB2ZXJzaW9uXCJdXG5cblxudHJpZ2dlciAtLT4gY2hlY2tfY2lyY2xlXG5cbmNoZWNrX2NpcmNsZSAtLT4gYnVpbGRfc2VydmVyXG5jaGVja19jaXJjbGUgLS0-IG5vdGlmeV9zdGFydFxuXG5idWlsZF9zZXJ2ZXIgLS0-IHRlc3Rfc2VydmVyXG5cbnRlc3Rfc2VydmVyIC0tXCI8aDI-bWFzdGVyPC9oMj5cIi0tPiByZXF1ZXN0X2FwcHJvdmFsXG50ZXN0X3NlcnZlciAtLVwiPGgyPm1hc3RlcjwvaDI-XCItLT4gcmVsZWFzZV9hcHByb3ZhbFxudGVzdF9zZXJ2ZXIgLS0-IG5vdGlmeV9zdWNjZXNzXG5cbnJlbGVhc2VfYXBwcm92YWwgLS0-IHB1Ymxpc2hfZ2l0aHViX3JlbGVhc2VcbnJlbGVhc2VfYXBwcm92YWwgLS0-IGRvY2tlcl9yZWxlYXNlXG5cbnB1Ymxpc2hfZ2l0aHViX3JlbGVhc2UgLS0-IG5vdGlmeV9yZWxlYXNlXG5kb2NrZXJfcmVsZWFzZS0tPiBub3RpZnlfcmVsZWFzZSIsIm1lcm1haWQiOnsidGhlbWUiOiJuZXV0cmFsIiwiYmFja2dyb3VuZENvbG9yIjoidHJhbnNwYXJlbnQifX0)