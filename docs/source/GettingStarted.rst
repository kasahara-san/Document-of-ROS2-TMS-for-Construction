Getting Started
===================================

本章ではROS2-TMS for Constructionのインストールから、ROS2-TMS for Constructionから
OperaSim-PhysX上の建設機械を実際に動作させるまでの流れを説明する。

インストール
===================================

以下のコマンドを実行する。::

      cd
      mkdir -p ~/ros2-tms-for-construction_ws/src && cd ~/ros2-tms-for-construction_ws/src
      git clone https://github.com/irvs/ros2_tms_for_construction.git
      cd ros2_tms_for_construction
      . setup.sh

.. _sample-task-execusion:

サンプルタスクを実行
===================================

1. 以下のコマンドを実行し、MongoDBを起動する。::
   
      sudo systemctl start mongod
   
2. 以下のコマンドを実行し、MongoDB Compassを起動する。::
   
      mongodb-compass
   
3. ポップアップするMongodbの画面にて、URIで"mongodb://localhost:27017/"と指定されていることを確認し、"Connect"ボタンをクリックすると表示される画面にて、rostmsdbをクリックして以下の画面が開けばデータベースの設定が完了している。

   もしデータベースが上記の表示にならない場合、データベースの構築ができておらず、このままでは正常にタスクを起動できない。
   この場合には以下のコマンドを実行する。::
       
      cd ~/ros2-tms-for-construction_ws/src/ros2_tms_for_construction/demo
      unzip rostmsdb_collections.zip
      mongorestore dump

4. データベースが正常に構築できていることを確認したら以下のコマンドを実行し、タスク管理機構を起動する。::

      cd ~/ros2-tms-for-construction_ws
      source install/setup.bash
      ros2 launch tms_ts_launch tms_ts_construction.launch.py task_id:=[タスクID]
    
    すると以下に示すGUIボタンが表示される。GUIボタンには2種類のボタンが搭載されており、緑の部分をクリックするとサンプルタスクが実行される。また、赤色の領域をクリックするとタスク実行を緊急停止させることができる。


    なお、データベースに格納されているサンプルタスクの概要は以下に示すとおりである。

タスクの可視化
===================================
    
BehaviorTree.CPPではGrootと呼ばれるGUIアプリケーションが存在する。Grootの機能は以下に示すとおりである。

- **Editor** : タスクを設計・編集する機能
- **Monitor** : 実行中のタスクを可視化する機能

本章では、Grootを使用したタスクの可視化について紹介する。実行手順は以下に示すとおりである。

1. Behavior Treeがタスクを実行している間、Grootと呼ばれるアプリケーションを使用してタスクが実行されていく様子を可視化することができる。GrootはROS2上で実装されており、以下のコマンドで起動することができる。::

      cd ~/ros2-tms-for-construction_ws
      ros2 run groot Groot

.. note::

   Monitor機能はBehavior Treeがタスクを実行している間のみ実行可能です。

2. Grootを起動すると、以下の画面が表示される。可視化機能の起動には"Monitor"と記載されている部分をクリックする。
3. すると以下の画面が表示されるので、以下に示すとおりIPアドレスとポートを指定し、"Connect"ボタンをクリックする。
   

   - Sensing IP : localhost
   - Publisher Port : 1666
   - Server Port : 1667
   
.. note::

   Publisher Port, Server Portの値は起動するtms_ts_managerによって異なるため注意してください。サンプルタスクの場合、`こちら <https://github.com/irvs/ros2_tms_for_construction/blob/main/tms_ts/tms_ts_manager/src/task_schedular_manager.cpp#L74>`_
   の部分でPublisher PortとServer Portを指定しています。

4. すると以下に示すとおり、実行中のタスクの様子が可視化される。緑色は実行後、橙色は実行中、青色は未実行を示す。

.. note::

   タスクが可視化されず、以下のポップアップウィンドウが表示される場合がある。これはBehavior Treeがタスクを実行されていない若しくは実行終了していた場合に表示される。
   このような場合、`こちら <sample-task-execusion_>`_ の手順にしたがって再度タスクを実行し、必ずBehavior Treeがタスクを実行している間に"Connect"ボタンを押してください。


タスクの作成
===================================

本章では、Grootを使用したタスク作成の手順について説明する。

1. 以下のコマンドを実行し、Grootを起動する。::

      cd ~/ros2-tms-for-construction_ws
      ros2 run groot Groot

2. Grootを起動すると、以下の画面が表示される。可視化機能の起動には"Monitor"と記載されている部分をクリックする。
3. そして表示された画面上で以下の手順でカスタムノードの追加を行う。ここでいうカスタムノードとはROS2-TMS for Construction
   で独自に用意したBehavior Treeノード(以降、BTノードと呼ぶ)のことを指す。

   すると、以下に示すように新たに複数のノードが追加される。
4. この状態で任意のタスクを構築していく。なお、Leaf Nodeの概要はこちらに、その他のカスタムノード及びBehavior Treeの標準ノードの
概要はこちらで説明したとおりである。これらのノードをもとにタスクを構築する。タスクの例を以下に示す。

.. note::

   タスクを構築する際には、タスクを構成するSubtask Nodeで使用するパラメータデータをデータベースのrostmsdbデータベース parameterコレクション下
   に置いておく必要があります。データベースの仕様及びLeaf Nodeで指定するパラメータの仕様についてはこちらをご覧ください。

5. Groot上でタスクを作成したあとは以下の手順に沿って、src/ros2_tms_for_construction/tms_ts/tms_ts_manager/configディレクトリ下にタスク列のxmlファイル
を出力します。

6. xml形式のタスク列を出力した後は、以下のコマンドを実行しデータベース上にタスクデータとして登録します。::
      
      cd ~/ros2-tms-for-construction_ws
      colcon build --packages-select tms_ts_manager
      ros2 run tms_ts_manager task_generator.py --ros-args -p bt_tree_xml_file_name:=[configディレクトリ以下のパス]
7. するとデータベース上のrostmsdbデータベースのtaskコレクション上に新たなタスクデータが作成され、`こちら <sample-task-execusion_>`_ の手順にそってBehavior Treeから実行できるようになります。

