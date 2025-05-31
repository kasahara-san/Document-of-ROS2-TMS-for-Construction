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

    
5. 
