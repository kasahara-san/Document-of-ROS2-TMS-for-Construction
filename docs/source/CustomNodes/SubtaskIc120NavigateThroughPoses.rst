subtask_ic120_follow_waypointsの概要
===================================

概要
-----------
共通制御信号対応クローラダンプIC120をナビゲーション操作するSubtask Nodeの1つ。
ダンプの移動経路をNavigate Through Posesに従って指定する。
Navigate Through Posesではsubtask_ic120_follow_waypoints同様に
経路上の複数点に沿ったナビゲーションを行うものの、経路上の経由地点では位置合わせのみを
行う。本ノードはOperaSim-PhysX/AGX及び実機に対応。

使用方法
-----------
- **model_name** : "ic120"と指定
- **record_name** : 接続するSubtask Nodeの仕様に合わせたパラメータデータのrecord_nameの値を指定
- **subtask_node** :  "subtask_ic120_nvigate_through_poses"と指定。

.. image:: ../images/SubtaskIc120NavigateTheoughPoses.png
   :alt: SubtaskIc120NavigateTheoughPoses
   :width: 400px
   :align: center  
  
.. raw:: html

.. raw:: html

   <br><br>

パラメータデータの仕様
-----------

各配列の要素番号NはN個目のウェイポイントの値として指定

.. image:: ../images/DB_SubtaskNavigateThroughPoses.png
   :alt: DB_SubtaskNavigateThroughPoses
   :width: 300px
   :align: center  

※_id, model_name. description, record_name等の共通仕様は除外

サンプル
-----------

**動作** : Map座標基準のx軸方向1m, 2m, 3m地点を経由して移動。各地点ではbase_linkとmapの姿勢を合わせる。

.. image:: ../images/Sample_SubtaskIc120NavigateThroughPoses.svg
   :alt: Sample_SubtaskIc120NavigateThroughPoses
   :width: 400px
   :align: center  
