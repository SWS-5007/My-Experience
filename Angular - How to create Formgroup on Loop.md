# How to create FormGroup on Loop?

> Class
```
export class SkillsComponent {
  skills = new FormArray([]);

  addSkill() {
    const group = new FormGroup({
      level: new FormControl(''),
      name: new FormControl('')
    });

    this.skills.push(group);
  }
}
```

>HTML
```
<div *ngFor="let skill of skills.controls;">
  <ng-container [formGroup]="skill">
    <input formControlName="level" />
    <input formControlName="name" />
  </ng-container>
</div>
```