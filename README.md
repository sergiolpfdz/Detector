# Detector
Es un detector
xml_dir = "anotación/lego/"
img_dir = "imágenes/lego/"
etiquetas = ["lego"]
tamanio = 416
mejores_pesos = "lego_rojo.h5"
 
def leer_anotaciones(ann_dir, img_dir, etiquetas=[]):
    todas_imgs = []
    etiquetas_vistas = {}
    
    para ann en ordenado (os.listdir (ann_dir)):
        img = {'objeto':[]}
 
        árbol = ET.parse(ann_dir + ann)
        
        para elemento en árbol.iter():
            si 'nombre de archivo' en elem.tag:
                img['nombre de archivo'] = img_dir + elem.text
            si 'ancho' en elem.tag:
                img['ancho'] = int(elemento.texto)
            si 'altura' en elem.tag:
                img['altura'] = int(elemento.texto)
            si 'objeto' en elem.tag o 'parte' en elem.tag:
                objeto = {}
                
                para atributo en lista (elemento):
                    si 'nombre' en attr.tag:
                        obj['nombre'] = atributo.texto
 
                        if obj['name'] en seen_labels:
                            etiquetas_vistas[obj['nombre']] += 1
                        más:
                            etiquetas_vistas[obj['nombre']] = 1
                        
                        si len(etiquetas) > 0 y obj['name'] no en las etiquetas:
                            descanso
                        más:
                            img['objeto'] += [obj]
                            
                    si 'bndbox' en attr.tag:
                        para dim en lista (attr):
                            si 'xmin' en dim.tag:
                                obj['xmin'] = int(round(float(dim.text)))
                            si 'ymin' en dim.tag:
                                obj['ymin'] = int(round(float(dim.text)))
                            si 'xmax' en dim.tag:
                                obj['xmax'] = int(round(float(dim.text)))
                            si 'ymax' en dim.tag:
                                obj['ymax'] = int(round(float(dim.text)))
 
        si len(img['objeto']) > 0:
            todas_imgs += [img]
                        
    devolver all_imgs, seen_labels
 
tren_imgs, tren_etiquetas = leer_anotaciones(xml_dir, img_dir, etiquetas)
print('imagenes',len(tren_imgs), 'etiquetas',len(tren_etiquetas))
