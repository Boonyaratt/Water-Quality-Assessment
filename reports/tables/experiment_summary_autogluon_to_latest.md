# Experiment Summary: AutoGluon To Baseline/Stacking Station-temporal Models

วันที่สรุป: 2026-07-13  
Dataset หลัก: `E:\Water Quality Research\Data\tabular_data_14\train\rswq_model_input_relaxed_s2_context_2562_2568.csv`

## 1. ภาพรวม

รายงานนี้สรุปการทดลองตั้งแต่ AutoGluon จนถึง notebook ล่าสุดที่ทำ baseline, stacking, temporal test และ station-temporal test

เป้าหมายหลักคือพิสูจน์ว่าได้ลองหลายแนวทางแล้ว:

- AutoGluon `best_quality`
- Feature set comparison: `S2 only`, `Context only`, `S2 + Context`
- Regression สำหรับ `DO`, `BOD`, `Turbidity`, `SS`, `TCB`, `FCB`
- NH3 classification ทั้งแบบ `3-class` และ `binary`
- Baseline ML: Ridge/ElasticNet, RandomForest, ExtraTrees, XGBoost, CatBoost
- Manual stacking ensemble
- Validation ทั้ง temporal และ station-temporal

ข้อควรตีความ:

- `Turbidity` และ `SS` เป็นกลุ่ม optical/near-direct target
- `DO`, `BOD`, `TCB`, `FCB`, `NH3` เป็น non-optical/proxy/risk target ไม่ควรอ้างว่า Sentinel-2 วัดได้โดยตรง
- ผลของ `TCB`, `FCB`, `NH3` ควรถูกตีความเป็น risk/proxy มากกว่า exact measurement

## 2. Dataset และ split ที่ใช้ร่วมกัน

Dataset relaxed:

- จำนวนข้อมูล: 390 rows
- จำนวน columns: 226
- Train temporal: พ.ศ. 2562-2566 = 276 rows
- Test temporal: พ.ศ. 2567-2568 = 114 rows

จำนวนข้อมูลรายปี:

| BE year | n |
|---:|---:|
| 2562 | 51 |
| 2563 | 85 |
| 2564 | 57 |
| 2565 | 29 |
| 2566 | 54 |
| 2567 | 68 |
| 2568 | 46 |

Station-temporal split ใน notebook ล่าสุด:

| Fold | Train rows | Test rows | Held-out stations |
|---:|---:|---:|---:|
| 1 | 187 | 38 | 9 |
| 2 | 187 | 38 | 9 |
| 3 | 183 | 38 | 10 |

แนวคิด station-temporal:

- Train ใช้ปี 2562-2566 เฉพาะ train stations
- Test ใช้ปี 2567-2568 เฉพาะ held-out stations
- จึงทดสอบทั้ง future generalization และ unseen-station generalization พร้อมกัน

## 3. Feature sets

### AutoGluon notebooks

AutoGluon ใช้ feature set:

| Feature set | จำนวน feature | หมายเหตุ |
|---|---:|---|
| S2 only | 32 | Sentinel-2 bands, indices, ratios, script formulas |
| Context only | 107 | rainfall, ERA5-Land hourly, JRC, SRTM, WorldCover, temporal/categorical season |
| S2 + Context | 139 | รวม S2 + context |

### Baseline/stacking notebook ล่าสุด

Notebook ล่าสุดใช้ numeric-only feature:

| Feature set | จำนวน feature | หมายเหตุ |
|---|---:|---|
| S2 only | 32 | เหมือนเดิม |
| Context only | 106 | ไม่ใช้ categorical `season_south_th` |
| S2 + Context | 138 | numeric S2 + numeric context |

เหตุผลที่ต่างจาก AutoGluon 1 feature:

- AutoGluon รองรับ categorical feature ได้ตรง จึงนับ `season_south_th`
- Notebook baseline ใช้ sklearn pipeline แบบ numeric-only เพื่อเลี่ยง encoding complexity และลดความเสี่ยงเรื่องการ preprocess ที่ไม่เท่ากัน
- ยังมี season signal ผ่าน `month`, `day_of_year`, `doy_sin`, `doy_cos`

## 4. Experiment matrix

| Experiment | Notebook / output | จุดประสงค์ | Dataset | Split | Feature set | Model | Targets |
|---|---|---|---|---|---|---|---|
| AutoGluon main | `train_autogluon_local_relaxed.ipynb` run `ag_relaxed_main_best_s2_context_best_quality_20260711_185242` | ทดสอบ AutoML แบบแรงบน feature รวม | relaxed | temporal 2562-2566 / 2567-2568 | S2 + Context | AutoGluon `best_quality`, WeightedEnsemble L2/L3 | 6 regression + NH3 classification |
| AutoGluon diagnostic | `train_autogluon_local_relaxed.ipynb` run `ag_relaxed_diagnostic_s2_context_only_best_quality_20260711_231732` | แยกดูว่า S2 หรือ Context ช่วย target ไหน | relaxed | temporal | S2 only, Context only | AutoGluon `best_quality`, WeightedEnsemble L2/L3 | 6 regression + NH3 classification |
| AutoGluon report | `03_autogluon_old_runs_result_report.ipynb` | รวมผล AutoGluon เก่าและ plot | relaxed | ใช้ผลเก่า | S2 only, Context only, S2 + Context | ไม่ train ใหม่ | รวม metrics/predictions/feature importance |
| Baseline + stacking latest | `04_baseline_stack_station_temporal_final_model.ipynb` | เทียบ baseline ML, stacking, temporal และ station-temporal | relaxed | temporal + station-temporal | S2 only, Context only, S2 + Context | Ridge, ElasticNet, RF, ExtraTrees, XGBoost, CatBoost, stacking | 6 regression + NH3 3-class + NH3 binary |

## 5. Experiment 1: AutoGluon main

Path:

`E:\Water Quality Research\Experiments\autogluon_tabular\runs\ag_relaxed_main_best_s2_context_best_quality_20260711_185242`

Config:

- Dataset: relaxed
- Feature set: `S2 + Context`
- Preset: `best_quality`
- Time limit: 1800 seconds ต่อ target-feature run
- Validation mode: internal validation inside train years
- Train/test:
  - Train: 2562-2566
  - Test: 2567-2568
- Regression:
  - raw: `DO`, `BOD`
  - `log1p`: `Turbidity`, `SS`, `TCB`, `FCB`
- NH3:
  - classification แบบเดิม
- Best model ส่วนใหญ่:
  - `WeightedEnsemble_L2`
  - `WeightedEnsemble_L3`

ผลสำคัญ:

| Target | Feature set | Best model | Transform | RMSE | R2 | Pearson r | Spearman r |
|---|---|---|---|---:|---:|---:|---:|
| BOD | S2 + Context | WeightedEnsemble_L2 | raw | 0.758 | 0.225 | 0.498 | 0.494 |
| DO | S2 + Context | WeightedEnsemble_L3 | raw | 0.893 | 0.416 | 0.673 | 0.595 |
| FCB | S2 + Context | WeightedEnsemble_L2 | log1p | 3122 | 0.025 | 0.466 | 0.555 |
| SS | S2 + Context | WeightedEnsemble_L2 | log1p | 56.69 | 0.136 | 0.402 | 0.709 |
| TCB | S2 + Context | WeightedEnsemble_L2 | log1p | 8362 | 0.084 | 0.394 | 0.640 |
| Turbidity | S2 + Context | WeightedEnsemble_L2 | log1p | 53.62 | 0.274 | 0.573 | 0.709 |

สรุป:

- AutoGluon ensemble ทำ temporal performance ได้ดี โดยเฉพาะ `DO`, `Turbidity`, `SS`
- `TCB`/`FCB` มี rank signal แต่ exact RMSE/R2 ยังอ่อน

## 6. Experiment 2: AutoGluon diagnostic feature sets

Path:

`E:\Water Quality Research\Experiments\autogluon_tabular\runs\ag_relaxed_diagnostic_s2_context_only_best_quality_20260711_231732`

Config ต่างจาก main:

- ใช้ feature set แยก:
  - `S2 only`
  - `Context only`
- ใช้ preset/time/split/target เหมือน AutoGluon main

Best AutoGluon result เมื่อนำทุก feature set มาเทียบ:

| Target | Best feature set | Best model | Transform | RMSE | R2 | Spearman r |
|---|---|---|---|---:|---:|---:|
| BOD | S2 only | WeightedEnsemble_L3 | raw | 0.726 | 0.290 | 0.517 |
| DO | S2 + Context | WeightedEnsemble_L3 | raw | 0.893 | 0.416 | 0.595 |
| FCB | Context only | WeightedEnsemble_L3 | log1p | 3115 | 0.029 | 0.511 |
| SS | S2 + Context | WeightedEnsemble_L2 | log1p | 56.69 | 0.136 | 0.709 |
| TCB | Context only | WeightedEnsemble_L2 | log1p | 8246 | 0.109 | 0.632 |
| Turbidity | S2 + Context | WeightedEnsemble_L2 | log1p | 53.62 | 0.274 | 0.709 |

สรุป:

- `DO`, `Turbidity`, `SS` ได้ประโยชน์จาก `S2 + Context`
- `TCB`, `FCB` ได้สัญญาณจาก context มากกว่า exact spectral feature
- `BOD` best เป็น `S2 only` แต่ยังต้องตีความเป็น proxy ไม่ใช่ direct retrieval

## 7. Experiment 3: AutoGluon report notebook

Notebook:

`E:\Water Quality Research\Notebooks\autogluon_tabular\03_autogluon_old_runs_result_report.ipynb`

Report output:

`E:\Water Quality Research\Experiments\autogluon_tabular\reports\relaxed_autogluon_old_runs_report`

สิ่งที่ทำ:

- ไม่ train model ใหม่
- รวม metrics จาก AutoGluon main และ diagnostic
- ลบ duplicate rows
- รวม predictions
- plot observed vs predicted
- plot metric comparison
- plot residual diagnostics
- รวม feature importance
- สรุป target-wise interpretation

NH3 classification จาก AutoGluon:

| Target | Feature set | Best model | Accuracy | Balanced accuracy | Macro F1 |
|---|---|---|---:|---:|---:|
| NH3 | Context only | WeightedEnsemble_L2 | 0.307 | 0.380 | 0.251 |
| NH3 | S2 + Context | WeightedEnsemble_L2 | 0.281 | 0.354 | 0.233 |
| NH3 | S2 only | WeightedEnsemble_L2 | 0.281 | 0.342 | 0.228 |

สรุป:

- NH3 แบบ classification เดิมยังไม่ดี
- จึงเป็นเหตุผลให้ notebook ล่าสุดลอง `NH3_binary`

## 8. Experiment 4: Baseline + stacking + station-temporal latest

Notebook:

`E:\Water Quality Research\Notebooks\autogluon_tabular\04_baseline_stack_station_temporal_final_model.ipynb`

Config:

- Dataset: relaxed
- SAVE_OUTPUTS: `False`
- ใช้ output cell เป็นหลัก ไม่ export ไฟล์เยอะ
- Feature sets:
  - S2 only
  - Context only
  - S2 + Context
- Temporal test:
  - Train: 2562-2566
  - Test: 2567-2568
- Station-temporal:
  - 3 folds
  - Test fold ละ 38 rows
- Regression models:
  - DummyMedian
  - Ridge
  - ElasticNet
  - RandomForest
  - ExtraTrees
  - XGBoost
  - CatBoost
  - Stacking_RidgeMeta
- Classification models:
  - DummyMostFrequent
  - LogisticRegression
  - RandomForest
  - ExtraTrees
  - XGBoost
  - CatBoost
  - Stacking_LogisticMeta

จำนวน experiment ที่รัน:

- `metrics_df`: 744 rows
- `preds_df`: 42,408 rows
- runtime: ประมาณ 14 นาที

### 8.1 Temporal results ที่ดีที่สุดใน notebook ล่าสุด

| Target | Best/near-best temporal model | Feature set | RMSE / score | R2 / metric | Spearman / F1 |
|---|---|---|---:|---:|---:|
| BOD | Stacking_RidgeMeta | S2 + Context | RMSE 0.770 | R2 0.200 | Spearman 0.438 |
| DO | RandomForest | S2 + Context | RMSE 0.890 | R2 0.420 | Spearman 0.593 |
| FCB | CatBoost | S2 + Context | RMSE 3058 | R2 0.065 | Spearman 0.571 |
| SS | Stacking_RidgeMeta | S2 + Context | RMSE 52.40 | R2 0.262 | Spearman 0.695 |
| TCB | Stacking_RidgeMeta / CatBoost close | Context/S2+Context | RMSE 8337-8476 | R2 0.060-0.090 | Spearman 0.642-0.656 |
| Turbidity | Stacking_RidgeMeta | S2 + Context | RMSE 54.05 | R2 0.262 | Spearman 0.697 |

### 8.2 Station-temporal results

Station-temporal ทดสอบยากกว่า temporal เพราะ test เป็นทั้งอนาคตและ station ที่ไม่เคยเห็น

| Target | Stronger station-temporal result | Feature set | Station-temporal signal |
|---|---|---|---|
| BOD | CatBoost | S2 + Context | RMSE 0.824, Spearman 0.344 |
| DO | No strong model | mostly S2/Context | RMSE ราว 1.2+, Spearman ต่ำ |
| FCB | Weak | S2 + Context / Context | Spearman ประมาณ 0.2-0.26 |
| SS | Ridge / RF / ExtraTrees | S2 or S2+Context | Spearman ประมาณ 0.54-0.64 |
| TCB | Weak-to-moderate | S2+Context | Spearman ประมาณ 0.3-0.39 |
| Turbidity | ElasticNet/Ridge/S2 models | S2 only | Spearman ประมาณ 0.59-0.63 |

สรุป station-temporal:

- `Turbidity` และ `SS` transfer ข้าม station ได้ดีที่สุด
- `DO` temporal ดี แต่ station-temporal อ่อนลงมาก แปลว่าอาจพึ่ง station/system pattern
- `TCB`/`FCB` exact regression ไม่ robust

### 8.3 NH3 results ล่าสุด

NH3 3-class:

| Setup | Best model | Feature set | Temporal F1 | Station-temporal F1 |
|---|---|---|---:|---:|
| NH3_3class | ExtraTrees / Logistic close | S2 + Context / Context | 0.368-0.425 | 0.352-0.412 |

NH3 binary:

| Setup | Best model | Feature set | Temporal accuracy | Temporal balanced accuracy | Temporal F1 | Station-temporal F1 |
|---|---|---|---:|---:|---:|---:|
| NH3_binary | ExtraTrees | S2 + Context | 0.614 | 0.683 | 0.613 | 0.627 |

สรุป NH3:

- `NH3_3class` ยังไม่ดีพอ
- `NH3_binary` ดีขึ้นชัดเจนและควรถูกใช้เป็น risk classification

## 9. Final selected config จาก notebook ล่าสุด

Notebook ล่าสุดเลือก final config โดยใช้ temporal + station-temporal robustness

| Target | Task | Feature set | Selected model | Transform | Temporal RMSE / score | Temporal R2 / metric | Station-temporal evidence |
|---|---|---|---|---|---:|---:|---|
| BOD | Regression | S2 + Context | CatBoost | raw | RMSE 0.771 | R2 0.197 | station RMSE 0.824, Spearman 0.344 |
| DO | Regression | S2 + Context | CatBoost | raw | RMSE 0.900 | R2 0.407 | station RMSE 1.317, Spearman 0.210 |
| FCB | Regression | S2 + Context | CatBoost | log1p | RMSE 3058 | R2 0.065 | station log RMSE 2.055, Spearman 0.220 |
| SS | Regression | S2 + Context | RandomForest | log1p | RMSE 59.04 | R2 0.063 | station log RMSE 0.741, Spearman 0.539 |
| TCB | Regression | S2 + Context | CatBoost | log1p | RMSE 8476 | R2 0.059 | station log RMSE 1.748, Spearman 0.388 |
| Turbidity | Regression | S2 only | Stacking_RidgeMeta | log1p | RMSE 57.31 | R2 0.170 | station log RMSE 0.823, Spearman 0.591 |
| NH3_3class | Classification | S2 + Context | ExtraTrees | label | Acc 0.482 | Macro F1 0.368 | station F1 0.352 |
| NH3_binary | Classification | S2 + Context | ExtraTrees | label | Acc 0.614 | Macro F1 0.613 | station F1 0.627 |

## 10. AutoGluon ensemble เทียบกับ notebook ล่าสุด

ประเด็นสำคัญ:

- AutoGluon ใช้ `WeightedEnsemble_L2/L3`
- Notebook ล่าสุดมี manual stacking แต่ไม่ได้เอา AutoGluon ensemble เข้า final selector
- ดังนั้น final config ล่าสุดเป็น best among manual baseline/stacking candidates ไม่ใช่ best among all experiments

เปรียบเทียบ temporal performance โดยสรุป:

| Target | AutoGluon best RMSE | Latest manual/baseline selected RMSE | หมายเหตุ |
|---|---:|---:|---|
| BOD | 0.726 | 0.771 | AutoGluon ดีกว่า |
| DO | 0.893 | 0.900 | ใกล้กันมาก |
| FCB | 3115 | 3058 | latest manual ดีกว่าเล็กน้อย |
| SS | 56.69 | 59.04 selected, แต่ stacking temporal best 52.40 | ต้องแยก temporal-best กับ robustness-selected |
| TCB | 8246 | 8476 | AutoGluon ดีกว่าเล็กน้อย |
| Turbidity | 53.62 | 57.31 selected, แต่ S2+Context stacking 54.05 | AutoGluon temporal ยังดีมาก |

ข้อสรุป:

- AutoGluon ensemble ยังควรถูกเก็บเป็น `temporal-best candidate`
- Notebook ล่าสุดมีคุณค่าเพราะเพิ่ม station-temporal robustness ซึ่ง AutoGluon เก่ายังไม่มี
- ควรรายงาน final 2 แบบ:
  - `Temporal-best`: รวม AutoGluon ensemble + manual models
  - `Robustness-checked`: manual models ที่ผ่าน station-temporal evaluation

## 11. Key findings

### 11.1 Target ที่ไปต่อได้

`Turbidity` และ `SS`:

- มี Spearman สูง
- station-temporal ยังพอ robust
- เหมาะที่สุดสำหรับไปต่อ image patch/CNN

`DO`:

- temporal performance ดีสุดในกลุ่ม non-optical proxy
- แต่ station-temporal อ่อน แปลว่าการ generalize ไป station ใหม่ยังน่ากังวล

### 11.2 Target ที่ควรปรับเป็น risk classification

`TCB`, `FCB`, `NH3`:

- exact regression ไม่แข็งแรง
- มี rank/proxy signal บางส่วน
- เหมาะกับ risk-screening มากกว่า exact value prediction

โดยเฉพาะ `NH3`:

- 3-class ไม่ดีพอ
- binary `low_censored` vs `elevated` ดีขึ้นชัดเจน

### 11.3 Stacking ไม่ได้ชนะทุก target

- Stacking ช่วยบาง target เช่น `SS` และ `Turbidity`
- แต่ไม่ได้ชนะทุก target
- ถ้า stacking ชนะนิดเดียวแต่ station-temporal ไม่ robust ควรเลือก model ที่ง่ายกว่า เช่น CatBoost/RF/ExtraTrees

## 12. ข้อเสนอสำหรับรายงานอาจารย์

สรุปที่ควรพูด:

1. ได้ทดลอง AutoGluon `best_quality` แล้ว โดยได้ ensemble model เป็น benchmark
2. ได้ทดลองแยก feature set แล้วว่า target ไหนใช้ S2/context/combined ดีกว่า
3. ได้ทดลอง baseline ML หลายตัวและ stacking แล้ว
4. ได้เพิ่ม station-temporal test เพื่อตรวจ unseen-station generalization
5. พบว่า performance ดีเฉพาะบางกลุ่ม target
6. ควรปรับ scope:
   - `Turbidity`, `SS`: regression + CNN/image patch ต่อได้
   - `DO`: proxy regression ได้ แต่ต้องระวัง transfer
   - `BOD`: proxy signal ปานกลาง
   - `TCB`, `FCB`, `NH3`: ควรเป็น risk classification มากกว่า exact regression

## 13. Recommended next step

หากต้องการ final model ที่ยุติธรรมที่สุด ควรเพิ่มอีก 1 notebook/section:

`05_compare_autogluon_vs_manual_final_selection.ipynb`

หน้าที่:

- โหลด AutoGluon temporal metrics/predictions
- โหลด manual baseline/stacking metrics จาก notebook ล่าสุด
- รวมเป็น final comparison table
- เลือก 2 final sets:
  - `temporal_best_model`
  - `station_temporal_robust_model`

ถ้าต้องการให้ AutoGluon มี station-temporal evidence ด้วย ต้องรัน AutoGluon เพิ่มแบบ station-temporal folds ซึ่งจะใช้เวลามากกว่า แต่จะ fair ที่สุด

