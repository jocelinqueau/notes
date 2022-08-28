# Min Max Clamp

[video](https://www.youtube.com/watch?v=U9VF-4euyRo)

⚠️ all this seems to mess with the calculation of width
to investigate 🤨

## Min

```css
[selector](.class, element, #id){
    //for example
    width:min(value1, value2, ...othersValues)
}
```

example

```css
.container{
    width:min(50%, 600px)
}
```

```css
.container{
    width:min(50%, 600px, 10rem)
}
```

equivalent to

```css
    .container{
    width:50%;
    max-width:600px;
    }
```

## Max

like min but the other way

```css
[selector](.class, element, #id){
    //for example
    width:max(value1, value2, ...othersValues)
}
```

example

```css
.container{
    width:max(50%, 600px)
}
```

```css
.container{
    width:max(50%, 600px, 10rem)
}
```

## You can nest min and max inside themselves

```css
[selector](.class, element, #id){
    //for example
    width:max(min(value1, value2) ...othersValues)
}
```

## Clamp

min max idealSize

```css
[selector](.class, element, #id){
    //for example
    width:clamp(25ch, 50ch, 66%)
}
```

setting a min-width is problably not a good idea in most cases, except font, because it's mean you probably need a breakpoint at some time