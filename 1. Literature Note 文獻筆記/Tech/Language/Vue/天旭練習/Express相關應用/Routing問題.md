---
tags: []
date: 2024-03-29
time: 14:37
---
[link](https://stackoverflow.com/questions/57764951/a-routing-problem-with-workbox-vuejs-in-production-and-express)

簡單來說，是讓所有網頁網址都可以回退到indexRouter。

Since `vue` router is handling page routing, you'll have to render `index` for all requested paths like:

```javascript
router.get('*', function(req, res, next) {
    res.render('index');
});

// in server
app.use('*', indexRouter);

// static
app.get('*', function(req, res) {
	res.sendFile(path.join(staticPath, 'index.html'));
})
```

If you're exposing other endpoints from server you'll have to mount this as the last route middleware like, say in your case:

```javascript
app.use('/notifications', usersNotifications);
app.use('*', indexRouter);
```

