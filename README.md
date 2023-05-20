# Processamento Multiespectral - Processamento e Implementação de Dados Multimodais para Análise de Vinhas

O processamento multiespectral é uma implementação no ROS Melodic para processamento e implementação de dados multimodais para análise de vinhedos. O foco principal do projeto é o desenvolvimento
de um método para o registro de imagens multimodais a fim de obter uma imagem tridimensional
reconstrução da vinha enriquecida com dados fotométricos ou radiométricos. Além disso, um
módulo de inteligência artificial é desenvolvido para processar conjuntamente imagens das diferentes modalidades
para uma análise detalhada da condição da planta.

## Índice

[Requisitos](#requirements)

[Pipeline](#pipeline)

[Instalação de pacotes](#packages-installation)

[Arquivos de origem](#arquivos de origem)

[Launch Files](#launch-files)

[Recursos](#recursos)

[Execução](#execução)

[Experiências de demonstração](#demo-experiments)

[Figuras](#figuras)

[Licença](#licença)

## Requisitos

### Programas

* ROS Melódico Morenia.
*Ubuntu 18.04.5 LTS.

### Hardware

* [CMS-V GigE Silios](CMS-SETUP.md) Câmera multiespectral.
* Sensor Microsoft Kinect V2: Câmera RGB-D.

## Pipeline

<p align="center">
     <img src="/data/images/img15.png" width="60%" title="Pipeline" />
</p>

## Instalação de Pacotes

Certifique-se de ter instalado a versão melódica dos pacotes abaixo.

* [ueye_cam](http://wiki.ros.org/ueye_cam): pacote ROS que envolve a API do driver para câmeras UEye da IDS Imaging Development Systems GMBH.

     ```
     $ cd ~/catkin_ws/src
     $ git clone https://github.com/anqixu/ueye_cam.git
     $ cd ~/catkin_ws
     $ catkin_make
     ```

* [iai_kinect2](https://github.com/code-iai/iai_kinect2): Pacote que fornece ferramentas para Kinect V2 como ponte entre kinect e ROS, calibração de câmeras, etc.

* [libfreenect2](https://github.com/OpenKinect/libfreenect2): Drivers para Kinect V2.

* [image_pipeline](http://wiki.ros.org/image_pipeline): Este pacote foi projetado para processar imagens brutas de câmeras em entradas úteis para algoritmos de visão: imagens mono/coloridas retificadas, imagens com disparidade estéreo e nuvens de pontos estéreo.

     ```
     $ cd ~/catkin_ws/src
     $ git clone https://github.com/ros-perception/image_pipeline.git
     $ cd ~/catkin_ws
     $ catkin_make
     ```

* [rosbridge_suite](http://wiki.ros.org/rosbridge_suite): pacote ROS que fornece uma API JSON para funcionalidade ROS para programas não-ROS.

     `$ sudo apt-get install ros-melodic-rosbridge-server`

* [rviz](http://wiki.ros.org/rviz): ferramenta de visualização 3D para ROS.

* [rtabmap_ros](http://wiki.ros.org/rtabmap_ros): Uma abordagem RGB-D SLAM com restrições em tempo real.

     `$ sudo apt-get install ros-melodic-rtabmap-ros`

## Arquivos Fonte

* band_separator.cpp: nó C++ para separação, pré-processamento e processamento de imagens multiespectrais. Fornece GUI para várias tarefas.
* band_separator.py: Nó Python para separação, pré-processamento e processamento de imagens multiespectrais. Fornece GUI para várias tarefas.
* backup.cpp: nó C++ para salvar quadros únicos ou fluxo de quadros.
* backup.py: nó Python para salvar quadros únicos ou fluxo de quadros.
* Experiments.cpp: Este nó publica imagens quando ao tópico que o nó band_separator subscreve. Pode ser usado quando nenhuma câmera está disponível.
* offline_registration.cpp: Nó para publicar os tópicos iamgem para uma simulação de registro de imagem offline.
* features_registraor.cpp: nó C++ que detecta características de 2 imagens e as alinha.
* features_registraor.py: nó Python que detecta recursos de 2 imagens e os alinha.
* corners_registraor.cpp: nó C++ que detecta características de 2 imagens e as alinha.
* corners_registraor.py: nó Python que detecta recursos de 2 imagens e os alinha.
*synchron.cpp: nó C++ que se inscreve em tópicos de imagem e os publica após a sincronização.
*synchron.py: Nó Python que se inscreve em tópicos de imagem e os publica após a sincronização.
* calibrator.py: Nó que realiza calibração.
* stereo_calibrator.py: Nó que realiza calibração estéreo.
* tf_node.cpp: Nó de transformação com C++.
* tf_node.py: Nó de transformação com Python.

## Arquivos de inicialização

* cms_cpp.launch: Executa câmera multiespectral, funcionalidades de pré-processamento com C++, conexão entre câmera e controlador.
* cms_py.launch: Executa câmera multiespectral, funcionalidades de pré-processamento com Python, conexão entre câmera e controlador.
* camera_configurator.launch: Executa câmera multiespectral, conexão entre câmera e controlador.
* kinect2_bridge.launch: Executa o kinect.
* point_cloud_generator.launch: Gera nuvens de pontos a partir de determinados tópicos.
* ueye_camera_gige.launch: Executa nodelet multiespectral para ligar a câmera.
* stereo_calibration.launch: Nó de calibração para câmeras estéreo.
* calibração.launch: Executa o nó de calibração para a câmera multiespectral.
* registration_approach1_cpp.launch: Arquivo de inicialização de registro de imagem para nó C++ com abordagem 1 (detecção de recurso).
* registration_approach1_py.launch: Lançamento de registro de imagem
