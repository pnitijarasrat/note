# Matching Date algorithms

> This algorithm handles matching dates between _date from board_ and _date displayed in operation sheet_

## Variable

- bd = boardDate
- dd = displayDate
- index = bd - 1

## Key Ideas

- round up the (bd-1)/7 = week

## Cautions

- week = 0 return dd = bd
- week > 0 return dd = bd + multiplier x week

### Microcode
