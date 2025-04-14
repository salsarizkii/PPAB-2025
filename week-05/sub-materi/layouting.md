#  Layouting dengan Jetpack Compose: ConstraintLayout

Jetpack Compose menyediakan `ConstraintLayout` untuk membuat layout yang fleksibel dan kompleks dengan pendekatan deklaratif.


---

##  Dasar ConstraintLayout

Gunakan `ConstraintLayout` dengan `createRefs()` dan `constrainAs()` untuk mengatur posisi komponen berdasarkan constraint.

```kotlin
@Composable
fun BasicConstraintLayout() {
    ConstraintLayout(
        modifier = Modifier.fillMaxSize()
    ) {
        val (button, text) = createRefs()

        Button(
            onClick = { /* aksi */ },
            modifier = Modifier.constrainAs(button) {
                top.linkTo(parent.top, margin = 16.dp)
                start.linkTo(parent.start)
                end.linkTo(parent.end)
            }
        ) {
            Text("Klik Saya")
        }

        Text(
            text = "Hello ConstraintLayout",
            modifier = Modifier.constrainAs(text) {
                top.linkTo(button.bottom, margin = 16.dp)
                start.linkTo(parent.start)
                end.linkTo(parent.end)
            }
        )
    }
}
```

---

##  Barrier

`Barrier` digunakan untuk membuat batas berdasarkan beberapa elemen.

```kotlin
@Composable
fun ConstraintWithBarrier() {
    ConstraintLayout(modifier = Modifier.fillMaxSize()) {
        val (button1, button2, text) = createRefs()

        Button(
            onClick = {},
            modifier = Modifier.constrainAs(button1) {
                top.linkTo(parent.top, margin = 16.dp)
                start.linkTo(parent.start, margin = 16.dp)
            }
        ) {
            Text("Button 1")
        }

        Button(
            onClick = {},
            modifier = Modifier.constrainAs(button2) {
                top.linkTo(button1.bottom, margin = 16.dp)
                start.linkTo(parent.start, margin = 32.dp)
            }
        ) {
            Text("Button 2")
        }

        val barrier = createEndBarrier(button1, button2)

        Text(
            "Text dengan Barrier",
            modifier = Modifier.constrainAs(text) {
                top.linkTo(parent.top, margin = 32.dp)
                start.linkTo(barrier, margin = 16.dp)
            }
        )
    }
}
```

---

##  Chain Layout

Gunakan `createHorizontalChain` atau `createVerticalChain` untuk menyusun elemen secara fleksibel.

```kotlin
@Composable
fun HorizontalChainLayout() {
    ConstraintLayout(modifier = Modifier.fillMaxSize()) {
        val (box1, box2, box3) = createRefs()

        createHorizontalChain(box1, box2, box3, chainStyle = ChainStyle.Spread)

        Box(
            modifier = Modifier
                .size(60.dp)
                .background(Color.Red)
                .constrainAs(box1) {
                    top.linkTo(parent.top, margin = 32.dp)
                }
        )

        Box(
            modifier = Modifier
                .size(60.dp)
                .background(Color.Green)
                .constrainAs(box2) {
                    top.linkTo(parent.top, margin = 32.dp)
                }
        )

        Box(
            modifier = Modifier
                .size(60.dp)
                .background(Color.Blue)
                .constrainAs(box3) {
                    top.linkTo(parent.top, margin = 32.dp)
                }
        )
    }
}
```

- `ChainStyle.Spread`: elemen tersebar merata
- `ChainStyle.SpreadInside`: elemen tersebar tapi tidak menyentuh ujung
- `ChainStyle.Packed`: elemen berhimpit

---

## 🔗 Referensi

- [ConstraintLayout - Jetpack Compose (Android Developers)](https://developer.android.com/develop/ui/compose/layouts/constraintlayout?hl=id)
- [Kode sumber contoh Compose ConstraintLayout](https://github.com/androidx/compose-samples)

```
