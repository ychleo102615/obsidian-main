---
tags: dailies  
date: {{date:YYYY-MM-DD}}
create: {{date:YYYY-MM-DD-ddd}}
time: {{time}}
create: <% tp.date.now("YYYY-MM-DD-ddd") %>
---

## Log
---


## Note
---


## Habit
---
- [ ] Reading
- [ ] English Pronouncing
- [ ] Facial
- [ ] Nofap
- [ ] Be nice


## Other
---

> [!Quote]+ Quote of the Day
> <% tp.web.daily_quote() %>

<< [[<% fileDate = moment(tp.file.title, 'YYYY-MM-DD').subtract(1, 'd').format('YYYY-MM-DD') %>|Yesterday]] | [[<% fileDate = moment(tp.file.title, 'YYYY-MM-DD').add(1, 'd').format('YYYY-MM-DD') %>|Tomorrow]] >>