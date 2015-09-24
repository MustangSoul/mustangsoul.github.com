---
layout:     post
title:      "黑板"
subtitle:   "工具"
date:       2015-09-24 19:00:00
author:     "ZhouYan"
header-img: "img/post-bg-05.jpg"
---

    public function do_ajax_saveShopCheckQuality()
    {
        $quality_score = $_POST['quality_score_val'];
        $pop_score = $_POST['pop_score'];
        $complex_score = $_POST['complex_score'];
        $checkNotes = $_POST['checkNotes'];
        $shop_id = $_POST['shop_id'];
        //未做审核或审核不通过，只修改质量分
        if($pop_score == 0 && $complex_score == 0){
            $upData = array('quality_score'=>$quality_score,'exe_val'=>2);
            $run = goodShopsModel::getInstance()->saveShopVerify($upData,$shop_id);
        }else{
            $upData['quality_score'] = $quality_score;
            $upData['pop_score'] = $pop_score;
            $upData['complex_score'] = $complex_score;
            $upData['exe_val'] = 2;

            if($complex_score == 4 || $complex_score == 3){
                $shopWeight = array('weight'=>100000,
                    'online'=>1,
                    'score'=>$complex_score,
                    'drop_weight'=>'0');
            }elseif($complex_score == 2){
                $shopWeight = array('weight'=>0,
                    'online'=>1,
                    'score'=>$complex_score,
                    'drop_weight'=>'0');
            }elseif($complex_score == 1){
                $shopWeight = array('weight'=>0,
                    'online'=>2,
                    'score'=>$complex_score,
                    'drop_weight'=>'1000000000');
            }

            //$shopWeight['create_time'] = date('Y-m-d H:i:s');
            $shopWeight['shop_id'] = $shop_id;

            $run = goodShopsModel::getInstance()->saveShopVerify($upData,$shop_id);
            goodShopsModel::getInstance()->inOnlineTable($shopWeight);
        }

        $re = array('succ'=>1);
        echo json_encode($re);
        exit;
    }