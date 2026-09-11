# Correção do bug de layout no Jetpack Compose

## Problema

O código original era:

```kotlin
Row(modifier = Modifier.fillMaxWidth()) {
    Text("Total")
    Text("R$ 42,90", Modifier.weight(1f))
}
```

O `weight(1f)` foi aplicado ao preço, fazendo o `Text` ocupar o espaço restante da `Row`.

## Solução 1 — Arrangement.SpaceBetween

```kotlin
Row(
    modifier = Modifier.fillMaxWidth(),
    horizontalArrangement = Arrangement.SpaceBetween
) {
    Text("Total")
    Text("R$ 42,90")
}
```

O `Arrangement.SpaceBetween` distribui os elementos nas extremidades da `Row`, deixando **Total** à esquerda e **R$ 42,90** à direita.

## Solução 2 — Spacer com weight

```kotlin
Row(
    modifier = Modifier.fillMaxWidth()
) {
    Text("Total")

    Spacer(
        modifier = Modifier.weight(1f)
    )

    Text("R$ 42,90")
}
```

Nessa solução, o `weight(1f)` é aplicado ao `Spacer`. Ele ocupa o espaço disponível entre os dois textos, empurrando o preço para a direita.

## Resultado

As duas soluções corrigem o problema e deixam:

**Total**                         **R$ 42,90**
