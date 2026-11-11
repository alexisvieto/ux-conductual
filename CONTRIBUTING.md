# Cómo contribuir

Gracias por querer mejorar UX Conductual. Para que la skill siga siendo útil y
confiable, cada aporte cumple tres reglas.

## 1. Evidencia

- Un principio nuevo trae al menos una fuente verificable (estudio, estándar o
  guía reconocida) en `references/fuentes.md`.
- Si la evidencia está en discusión, dilo en el propio principio.
- Los números que son heurísticas se marcan como heurísticas.

## 2. Formato

- Cada principio sigue la estructura: **Qué es**, **Por qué funciona**, **Cómo
  aplicarlo**, **La trampa**, **Regla**.
- Cada tipo de pantalla del playbook sigue: **Principios**, **Patrones**,
  **Evita**.
- Español neutro, tuteo, frases cortas. Sin modismos de un solo país.
- `SKILL.md` se mantiene corto: el detalle va en `references/`.

## 3. Pruebas

- Si agregas o cambias comportamiento, agrega o actualiza un caso en
  `evals/evals.json` con lo que se espera.
- Prueba la skill en Claude Code con al menos un caso real antes de abrir el PR.

## Proceso

1. Abre un issue describiendo el cambio, salvo que sea una corrección menor.
2. Haz un fork, crea una rama y abre un pull request.
3. Actualiza `CHANGELOG.md`.

Al contribuir aceptas que tu aporte se publique bajo la licencia
[CC BY 4.0](LICENSE).
