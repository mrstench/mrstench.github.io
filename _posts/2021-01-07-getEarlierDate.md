---
layout: post title: '获取本日/本周/本月/本年之前N日/N周/N月/N年的开始时间和结束时间（时间戳）' subtitle: ''
date: 2021-04-14 author: mrstench categories: PHP
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-theme-h2o-postcover.jpg'
tags: PHP
---

```phpt
    <?php

    declare(strict_types=1);
    
    date_default_timezone_set('PRC');
    
    /**
     * 获取本日/本周/本月/本年之前N日/N周/N月/N年的开始时间和结束时间（时间戳）
     * @param string $dateType
     * @param int $num
     * @return array
     */
    function getEarlierDate(string $dateType, int $num): array
    {
        $w = (int)date('w');
        $y = (int)date('Y');
        $m = (int)date('m');
        $d = (int)date('d');
    
        $date = [];
        switch ($dateType) {
            case 'day':
                for ($i = $num - 1; $i >= 0; $i--) {
                    $startDate = mktime(0, 0, 0, $m, $d - $i, $y);
                    $endDate = mktime(23, 59, 59, $m, $d - $i, $y);
                    $date[] = [
                        'startTime' => $startDate,
                        'endTime' => $endDate,
                    ];
                }
                break;
            case 'week':
                for ($i = $num - 1; $i >= 0; $i--) {
                    $startDate = mktime(0, 0, 0, $m, $d - $w + 1 - $i * 7, $y);
                    $endDate = mktime(23, 59, 59, $m, $d - $w + 7 - $i * 7, $y);
                    $date[] = [
                        'startTime' => $startDate,
                        'endTime' => $endDate,
                    ];
                }
                break;
            case 'month':
                for ($i = $num - 1; $i >= 0; $i--) {
                    $startDate = mktime(0, 0, 0, $m - $i, 1, $y);
                    $endDate = mktime(0, 0, 0, $m + 1 - $i, 1, $y) - 1;
                    $date[] = [
                        'startTime' => $startDate,
                        'endTime' => $endDate,
                    ];
                }
                break;
            case 'year':
                for ($i = $num - 1; $i >= 0; $i--) {
                    $startDate = mktime(0, 0, 0, 1, 1, $y - $i);
                    $endDate = mktime(0, 0, 0, 1, 1, $y + 1 - $i) - 1;
                    $date[] = [
                        'startTime' => $startDate,
                        'endTime' => $endDate,
                    ];
                }
                break;
            default:
                $date = [];
        }
        return $date;
    }

```
    
