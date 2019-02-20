---
description: >-
  JOBSHEET 4 Displaying Data And Handling Events Mata Kuliah Pemrograman Web
  Lanjut
---

# JOBSHEET 4 WEB

  
**Praktikum - Bagian 1: Component Basic**

Menambahkan code pada courses.component.ts

{% code-tabs %}
{% code-tabs-item title="courses.component.ts" %}
```typescript
import { Component, OnInit } from '@angular/core';
import { CoursesService } from '../courses.service';

@Component({
  selector: 'app-courses',
  templateUrl: './courses.component.html',
  styleUrls: ['./courses.component.css']
})
export class CoursesComponent implements OnInit {

  title = 'Belajar Angular';
  Courses;
  binding = 'property-binding';
  imageUrl = 'http://lorempixel.com/400/200';

  constructor(private service:CoursesService) {
    this.Courses = service.getCourses();
   }

  ngOnInit() {
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Menambahkan code pada courses.component.html

{% code-tabs %}
{% code-tabs-item title="courses.component.html" %}
```markup
<p>
  {{ title }}
</p>
<table>
  <thead>
    <th>
      #ID
    </th>
    <th>
      Course name
    </th>
  </thead>
  <tbody>
    <tr *ngFor="let Course of Courses">
      <td>{{ Course.id }}</td>
      <td>{{ Course.name }}</td>
    </tr>
  </tbody>
</table>

```
{% endcode-tabs-item %}
{% endcode-tabs %}

Soal-1 :

![Gambar 1: Hasil dari Component Basic](.gitbook/assets/1.jpg)

**Praktikum - Bagian 2: Attribute Binding**

Menambahkan `colSpan = 2;`Pada line 15 di courses.component.ts

Menambahkan code untuk membuat table pada courses.component.html

{% code-tabs %}
{% code-tabs-item title="courses.component.html" %}
```markup
<table>
  <tr>
    <td [colspan] = 'colSpan'></td>
  </tr>
</table>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Error akan muncul seperti ini

![Gambar 2: Error karena attribute colspan tidak diketahui](.gitbook/assets/image%20%284%29.png)

Untuk memperbaiki tambah "attr." sebelum colspan

{% code-tabs %}
{% code-tabs-item title="courses.component.html" %}
```markup
<table>
  <tr>
    <td [attr.colspan] = 'colSpan'></td>
  </tr>
</table>
```
{% endcode-tabs-item %}
{% endcode-tabs %}



Soal-2:

![Gambar 3: localhost kembali berjalan](.gitbook/assets/image%20%2811%29.png)

Soal-3:

Membuat button `<button class = "btn btn-primary" type = "button">Tambah</button>`

![Gambar 4: Hasil dari Attribute Binding](.gitbook/assets/2.jpg)

**Praktikum - Bagian 3: Class Binding**

Menambahkan  `isActive = true;`pada courses.component.ts di line 16

Menambahkan code dibawah tabel pertama :

{% code-tabs %}
{% code-tabs-item title="courses.component.html" %}
```markup
<h2>property-binding</h2>
<h2>property-binding</h2>
<img src="http://lorempixel.com/400/200">
<img src="http://lorempixel.com/400/200">
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Mengubah  `isActive = true;` menjadi  `isActive = false;`

**Praktikum - Bagian 4: Style Binding**

`<button class = "btn btn-primary" type="button" [style.backgroundColor] = "isActive?'blue' : 'white'">Tambah</button>`

Soal-4:

![Gambar 5: Hasil dari Style Binding](.gitbook/assets/image%20%285%29.png)

**Praktikum - Bagian 5: Event Binding**

Menambahkan code `onSave() { console.log("button sudah di klik") }`pada baris 18

Menambahkan code `<button type="button" class = "btn btn-default" (click) = "onSave()">Button</button>` pada baris 33

![Gambar 6: Memunculkan console log pada button](.gitbook/assets/image%20%2814%29.png)

Menambahkan parameter `$event` pada method `onSave()`

{% code-tabs %}
{% code-tabs-item title="courses.component.ts" %}
```typescript
onSave($event) {
    console.log("button sudah di klik", $event)
  }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Menambah code pada button ke-3

`<button type="button" class = "btn btn-danger" (click) = "onSave($event)">Button</button>`

Soal-5:

![Gambar 7: Hasil dari method onSave\(\) dengan parameter $event](.gitbook/assets/image%20%288%29.png)

Menambahkan method `onDivClick()` dibawah method `onSave()`

{% code-tabs %}
{% code-tabs-item title="courses.component.ts" %}
```typescript
onDivClick($event) {
    console.log("ini method div", $event)
  }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Membuat button dengan div

{% code-tabs %}
{% code-tabs-item title="courses.component.html" %}
```markup
<div (click) = "onDivClick($event)">
  <button type="button" class="btn btn-danger" (click) = "onSave($event)">button</button>
</div>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Soal-6:

![Gambar 8: Hasil dari pembuatan button dengan 2 method. Yaitu onDivClick\(\) dan onSave\(\)](.gitbook/assets/image%20%287%29.png)

**Penjelasan**: Console.log muncul 2 pesan ya itu mengenali method onDivClick\(\) dan onSave\(\) jadi kedua method akan terpanggil dalam ketukan pada button

Menambahkan `$event.stopPropagation();` pada method onSave\(\) untuk mengatasi masalah diatas

Soal-7:

![Gambar 9: Dengan stopPropagation\(\) maka event pada method onDivClik\(\) tidak akan terpanggil](.gitbook/assets/image%20%2813%29.png)

**Penjelasan:** Kegunaan dari stopPropagation\(\) adalah untuk mengatasi terjadinya pengenalan pada event method selanjutnya \(hanya pada parent method\)



**Praktikum - Bagian 6: Event Binding**

Membuat input berupa keyup `<input type = "text" (keyup.enter) = "onekeyUp()">`

Membuat method onekeyUp\(\)

{% code-tabs %}
{% code-tabs-item title="courses.component.ts" %}
```typescript
  onkeyUp() {
    console.log("enter was pressed");
  }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Soal-8 dan Soal-9:

![Gambar 10: Hasil dari Event Binding](.gitbook/assets/image%20%2812%29.png)

**Praktikum - Bagian 7: Template Binding**

Tambahkan `#nama` pada input `<input type = "text" #nama (keyup.enter) = "onkeyUp()(nama.value)">`

Memberi parameter pada method onkeyUp\(\)

{% code-tabs %}
{% code-tabs-item title="courses.component.ts" %}
```typescript
  onkeyUp(nama) {
    console.log(nama);
  }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Soal-10

![Gambar 11: Hasil dari Tempalte Binding](.gitbook/assets/image%20%289%29.png)

**Penjelasan:** Jika kolom input diisi dengan text, lalu tekan enter, maka isi dari kolom tersebut akan muncul di consol.

**Praktikum - Bagian 8: Two Way Binding**

Membuat attribute baru `nama = 'Alan';` dan ubah parameter pada method onkeyUp\(\)

{% code-tabs %}
{% code-tabs-item title="courses.component.ts" %}
```typescript
onkeyUp() {
    console.log(this.nama);
  }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Ubah tag input menjadi `<input type="text" [value] = 'nama' (keyup.enter) = "nama = $event.target.value;onkeyUp()">`

Soal-11:

![Gambar 12: Hasil dari Two Way Binding](.gitbook/assets/image%20%2816%29.png)

**Penjelasan:** Isi dari atrribute nama akan di tampilkan pada kolom input dengan `$event.target.value`. 

Meng-edit file app.module.ts mendjadi seperti berikut

{% code-tabs %}
{% code-tabs-item title="app.module.ts" %}
```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { CoursesComponent } from './courses/courses.component';
import { CoursesService } from './courses.service';

@NgModule({
  declarations: [
    AppComponent,
    CoursesComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    FormsModule
  ],
  providers: [CoursesService],
  bootstrap: [AppComponent]
})
export class AppModule { }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Tambahkan code berikut pada courses.component.html `<input type="text" [(ngModel)] = "nama" (keyup.enter)="onkeyUp()">`

Soal-12:

![Gambar 13: Element hasil dari Two Way Binding](.gitbook/assets/image%20%281%29.png)

**Penjelasan:** ngModel membuat form control dari sebuah domain dan akan mem-bind menjadi form control element. \(Untuk soal 11 dan 12 perbedaannya adalah pada soal 11 tidak terdapat ng-reflect-model, sedangkan 12 ada ng-reflect-model yang mana kolom tersebut sudah menjadi FormControl\).

