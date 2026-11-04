# Diccionario de exclusión

Lista de términos que se excluyen del vocabulario antes de construir los tópicos (Sección 3.5.2 de la tesis). Es la unión de siete conjuntos: 454 entradas en total, 449 únicas, porque algunos términos pertenecen a más de un conjunto. El código la arma en cada notebook de técnica, en la celda de configuración (`CONTEXTO`, `SENTIMIENTO`, `ERRORES`, `CORTESIA`, `LUGARES` y los identificadores de parque), y la imprime completa en `03_LDA.ipynb`.

| Conjunto | Entradas |
|---|---:|
| Palabras funcionales del español de NLTK | 306 |
| Términos de contexto del dominio | 70 |
| Términos de valoración | 55 |
| Variantes ortográficas y error de lematización | 11 |
| Fórmula de cortesía | 1 |
| Topónimo adicional | 1 |
| Identificadores de parques | 10 |
| **Suma de los conjuntos** | **454** |
| **Entradas únicas** | **449** |

Todas las entradas están sin tildes, como las compara el código.

## 1. Palabras funcionales del español de NLTK

Lista `stopwords.words('spanish')` de NLTK, sin tildes; las formas que coinciden al quitar las tildes cuentan una sola vez.

a, al, algo, algunas, algunos, ante, antes, como, con, contra, cual, cuando, de, del, desde, donde, durante, e, el, ella, ellas, ellos, en, entre, era, erais, eramos, eran, eras, eres, es, esa, esas, ese, eso, esos, esta, estaba, estabais, estabamos, estaban, estabas, estad, estada, estadas, estado, estados, estais, estamos, estan, estando, estar, estara, estaran, estaras, estare, estareis, estaremos, estaria, estariais, estariamos, estarian, estarias, estas, este, esteis, estemos, esten, estes, esto, estos, estoy, estuve, estuviera, estuvierais, estuvieramos, estuvieran, estuvieras, estuvieron, estuviese, estuvieseis, estuviesemos, estuviesen, estuvieses, estuvimos, estuviste, estuvisteis, estuvo, fue, fuera, fuerais, fueramos, fueran, fueras, fueron, fuese, fueseis, fuesemos, fuesen, fueses, fui, fuimos, fuiste, fuisteis, ha, habeis, habia, habiais, habiamos, habian, habias, habida, habidas, habido, habidos, habiendo, habra, habran, habras, habre, habreis, habremos, habria, habriais, habriamos, habrian, habrias, han, has, hasta, hay, haya, hayais, hayamos, hayan, hayas, he, hemos, hube, hubiera, hubierais, hubieramos, hubieran, hubieras, hubieron, hubiese, hubieseis, hubiesemos, hubiesen, hubieses, hubimos, hubiste, hubisteis, hubo, la, las, le, les, lo, los, mas, me, mi, mia, mias, mio, mios, mis, mucho, muchos, muy, nada, ni, no, nos, nosotras, nosotros, nuestra, nuestras, nuestro, nuestros, o, os, otra, otras, otro, otros, para, pero, poco, por, porque, que, quien, quienes, se, sea, seais, seamos, sean, seas, sentid, sentida, sentidas, sentido, sentidos, sera, seran, seras, sere, sereis, seremos, seria, seriais, seriamos, serian, serias, si, siente, sin, sintiendo, sobre, sois, somos, son, soy, su, sus, suya, suyas, suyo, suyos, tambien, tanto, te, tendra, tendran, tendras, tendre, tendreis, tendremos, tendria, tendriais, tendriamos, tendrian, tendrias, tened, teneis, tenemos, tenga, tengais, tengamos, tengan, tengas, tengo, tenia, teniais, teniamos, tenian, tenias, tenida, tenidas, tenido, tenidos, teniendo, ti, tiene, tienen, tienes, todo, todos, tu, tus, tuve, tuviera, tuvierais, tuvieramos, tuvieran, tuvieras, tuvieron, tuviese, tuvieseis, tuviesemos, tuviesen, tuvieses, tuvimos, tuviste, tuvisteis, tuvo, tuya, tuyas, tuyo, tuyos, un, una, uno, unos, vosotras, vosotros, vuestra, vuestras, vuestro, vuestros, y, ya, yo.

## 2. Términos de contexto del dominio

aca, ahi, ahora, alguno, alla, ano, asi, aunque, capital, caso, ciudad, cosa, dar, deber, decir, dejar, dia, encontrar, espacio, estar, etc, fin, gente, haber, hacer, ir, llegar, llevar, lugar, mate, medio, mismo, momento, montevideo, noche, pais, parecer, parque, parte, pasar, pasear, paseo, persona, poder, poner, publico, pues, quedar, querer, saber, salir, seguir, semana, ser, siempre, sino, sitio, solo, tal, tan, tema, tener, tipo, uruguay, venir, ver, vez, visita, visitar, zona.

## 3. Términos de valoración

agradable, bastante, bello, bien, bonito, buen, bueno, desagradable, desastre, destacar, disfrutable, disfrutar, divino, encantar, espantoso, espectacular, excelente, fantastico, feo, genial, gran, grande, gustar, hermoso, horrible, ideal, impecable, impresionante, increible, lamentable, lindo, mal, malo, maravilloso, mayor, mejor, menor, mucho, muy, patetico, paz, pena, peor, perfecto, pesimo, poco, precioso, recomendable, recomendado, recomendar, relax, super, terrible, tranquilo, valer.

## 4. Variantes ortográficas y error de lematización

ermosa, ermoso, escelente, exelente, exelentes, imprecionante, lindar, mas, recomeir, recomendacion, recomiendable.

Las formas se conservan tal como figuran en el código. «lindar» es el lema que spaCy asigna erróneamente a las formas de «lindo».

## 5. Fórmula de cortesía

gracias.

## 6. Topónimo adicional

prado.

## 7. Identificadores de parques

botanico, espacio_modelo, idea_vilarinio, jose_batlle_y_ordoniez, museo_y-parque_fernando_garcia, parque_prado, parque_rodo, punta_yeguas, rosedal-del_prado, villa_dolores.

**Estas diez entradas no filtran los nombres de los parques.** Son los identificadores del conjunto de datos, cadenas sin espacios que no coinciden con ningún token del texto procesado. Solo «botanico», que es un token simple, resulta efectivamente excluido. Los componentes de los demás nombres («rosedal», «rodo», «batlle», «dolores», «yeguas», entre otros) permanecen en el vocabulario. La tesis lo declara en la Sección 3.5.2 y cuantifica su efecto en la Sección 4.2.1.
