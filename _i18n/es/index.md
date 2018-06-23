El factor-iOS estuvo inspirado en el famoso framework [twelve-factor app](https://www.12factor.net/), una metodología para escribir servicios web de alta calidad. El factor-iOS usa la misma estructura y principios similares, reescritos y aplicados a los procesos de desarrollo de aplicaciones iOS.

## Contexto

A los largo de los últimos 10 años, el proceso de desarrollo iOS ha variado drasticamente:

- desde soportar un sólo dispositivo hasta alcanzar un gran rango de iPhones y iPads disponibles con iOS y diferentes plataformas como tvOS y watchOS
- desde incluir submódulos de git manualmente hasta la utilización de gestores de dependencias
- desde aplicaciones iOS corriendo la mayoría de casos localmente _on-device_, hasta aplicaciones iOS totalmente dependientes de servicios back-end
- desde tiempos de revisión para aplicaciones iOS de más de 2 semanas hasta revisiones en menos de un dia
- desde instalaciones de aplicaciones en un dispositivo movil utilizando iTunes hasta la distribución de aplicaciones a través del canal oficial TestFlight
- desde los 5 screenshots por cada idioma en iTunes Connect hasta los 110 por idioma, además de la vista previa de aplicaciones
- desde aplicaciones Objective-C/C++ planas hasta una mezcla de lenguajes incluyendo JavaScript
- de publicaciones lentas cada que algo está listo, a despliegues semanales
- de publicaciones completas hasta tests A/B, entregas graduales y detección automática de regresiones

## Qué es el factor-iOS?

El factor-iOS es un proyecto experimental iniciado en mayo de 2018. Éste trata de proporciona una colección de mejores prácticas para la construcción de aplicaciones iOS de alta calidad. Cáda temática está cubierta por un `factor`, el cual describe un estado ideal de cómo podría parecer cierta categoría del proceso de desarrollo de una aplicación iOS.

Debido a ciertas limitaciones (como Xcode solo funcionando en macOS) no se pueden satisfacer todos los requisitos. Este proyecto intenta definir tanto objetivos, como también la mejor manera de resolver algunos de los retos que enfrentamos.

El factor-iOS contiene un marco más amplio de los procesos de desarrollo y decisiones arquitectónicas en aplicaciones iOS y no cubrirá ningún reto de algún lenguaje en específico.

Éste es un proyecto viviente, mantenido por la comunidad de desarrolladores iOS. Puedes encontrar el código fuente completo en [GitHub](https://github.com/ios-factor/ios-factor.com), actualizar páginas existentes o agregar nuevos factores.

-----
