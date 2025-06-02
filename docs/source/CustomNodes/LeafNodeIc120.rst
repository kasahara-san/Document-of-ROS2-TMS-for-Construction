LeafNodeIc120
===================================

概要
-----------
共通制御信号対応クローラダンプIC120を操作するSubtask Nodeを接続するLeaf Node。
OperaSim-PhysX/AGX及び実機に対応。

.. image:: ../images/LeafNodeIc120.png
   :alt: LeafNodeIc120
   :width: 200px
   :align: center  
  
.. raw:: html

.. raw:: html

   <br><br>

入力ポート
-----------
- **model_name** : "ic120"と指定
- **record_name** : 接続するSubtask Nodeの仕様に合わせたパラメータデータのrecord_nameの値を指定
- **subtask_node** :  :doc:`subtask_ic120_navigate_anywhere <SubtaskIc120NavigateAnywhere>`, :doc:`subtask_ic120_follow_waypoints <SubtaskIc120FollowWaypoints>`, :doc:`subtask_ic120_navigate_through_poses <SubtaskIc120NavigateThroughPoses>`, :doc:`subtask_ic120_release_soil <SubtaskIc120ReleaseSoil>`  のいずれかを指定

IC120
-----------

.. image:: ../images/Ic120.png
   :alt: Ic120
   :width: 200px
   :align: center  
