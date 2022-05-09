# Daily Workout Log

```button
name Add Exercise
type command
action QuickAdd: Add Exercise
color blue
```
^button-8s0k

```dataviewjs
let pages = dv.pages("#workouts").where(b => b.date_of_workout >= DateTime.now().minus({weeks:1})).groupBy(b => b.date_of_workout)

for (let group of pages.sort(d => d.key, 'desc')) { 
	dv.header(6, group.key);
	dv.table(["File", "Exercise", "Set", "Reps", "Time", "Weight"], 
		group.rows 
			.sort(k => k.type, 'asc')
			.map(k => [k.file.link, k["exercise"], k["sets"], k["reps"], k["time"], k["weight"]]))
}
```