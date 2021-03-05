CSS TRICKS - FLEX BOX attribute
-------------


[csstrickslink]: https://css-tricks.com/snippets/css/a-guide-to-flexbox/ "CSS-Tricks flexbox"


``` css

.container{
  display: flex;
  flex-direction: row;
  flex-wrap: /* nowrap  */wrap;
  /* flex-flow: column wrap; */
  /* justify-content: space-around; */
  /* justify-content: space-evenly; */
  justify-content: space-between;
  /* align-items: center; */
  /* align-items: baseline; */
  align-content: center;
}

.item{
    flex-basis: 60%;
    flex-grow: 1; /* default 0 */
    flex-shrink: 1; /* default 0 */
    /* align-self: ceneter; */
}
```
