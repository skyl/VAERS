
.. code:: python

    import pandas as pd
.. code:: python

    data = pd.DataFrame.from_csv("./1999VAERSData/1999VAERSDATA.csv")
    vax = pd.DataFrame.from_csv("./1999VAERSData/1999VAERSVAX.csv")
    symptoms = pd.DataFrame.from_csv("./1999VAERSData/1999VAERSSYMPTOMS.csv")
.. code:: python

    # Let's check out 117908 in depth
    print(data.ix[117908])
    data.ix[117908].SYMPTOM_TEXT

.. parsed-literal::

    RECVDATE                                               01/05/1999
    STATE                                                          CA
    AGE_YRS                                                       0.9
    CAGE_YR                                                         0
    CAGE_MO                                                       0.9
    SEX                                                             F
    RPT_DATE                                               12/28/1998
    SYMPTOM_TEXT    pt recv vax 27OCT98  & 10NOV severe vomiting, ...
    DIED                                                            Y
    DATEDIED                                               12/12/1998
    L_THREAT                                                      NaN
    ER_VISIT                                                      NaN
    HOSPITAL                                                      NaN
    HOSPDAYS                                                      NaN
    X_STAY                                                        NaN
    DISABLE                                                       NaN
    RECOVD                                                          N
    VAX_DATE                                               10/27/1998
    ONSET_DATE                                             11/10/1998
    NUMDAYS                                                        14
    LAB_DATA        glucose on admission 1310;NA 124;BUN 31;SGPT 2...
    V_ADMINBY                                                     PVT
    V_FUNDBY                                                      PVT
    OTHER_MEDS                                      Beclovent inhaler
    CUR_ILL                                                       NaN
    HISTORY         asthma, rt lower lobe infiltrate, innocent murmur
    PRIOR_VAX                                                    NONE
    SPLTTYPE                                                      NaN
    Name: 117908, dtype: object




.. parsed-literal::

    'pt recv vax 27OCT98  & 10NOV severe vomiting, glucose 92, felt prob viral age;25NOV seen for OM;29NOV cranky, some vomiting w/nl exam;sl weight loss;3DEC vomited againx2;dx DKA w/glucose 1310;'



.. code:: python

    vax[vax.index == 117908]



.. raw:: html

    <div style="max-height:1000px;max-width:1500px;overflow:auto;">
    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>VAX_TYPE</th>
          <th>VAX_MANU</th>
          <th>VAX_LOT</th>
          <th>VAX_DOSE</th>
          <th>VAX_ROUTE</th>
          <th>VAX_SITE</th>
          <th>VAX_NAME</th>
        </tr>
        <tr>
          <th>VAERS_ID</th>
          <th></th>
          <th></th>
          <th></th>
          <th></th>
          <th></th>
          <th></th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>117908</th>
          <td> FLU3</td>
          <td> PFIZER\WYETH</td>
          <td> 4988202</td>
          <td> 0</td>
          <td> IM</td>
          <td> LL</td>
          <td> INFLUENZA (SEASONAL) (FLUSHIELD)</td>
        </tr>
      </tbody>
    </table>
    <p>1 rows × 7 columns</p>
    </div>



.. code:: python

    symptoms[symptoms.index == 117908]



.. raw:: html

    <div style="max-height:1000px;max-width:1500px;overflow:auto;">
    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>SYMPTOM1</th>
          <th>SYMPTOMVERSION1</th>
          <th>SYMPTOM2</th>
          <th>SYMPTOMVERSION2</th>
          <th>SYMPTOM3</th>
          <th>SYMPTOMVERSION3</th>
          <th>SYMPTOM4</th>
          <th>SYMPTOMVERSION4</th>
          <th>SYMPTOM5</th>
          <th>SYMPTOMVERSION5</th>
        </tr>
        <tr>
          <th>VAERS_ID</th>
          <th></th>
          <th></th>
          <th></th>
          <th></th>
          <th></th>
          <th></th>
          <th></th>
          <th></th>
          <th></th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>117908</th>
          <td> Agitation</td>
          <td> 8.1</td>
          <td> Alanine aminotransferase increased</td>
          <td> 8.1</td>
          <td> Aspartate aminotransferase increased</td>
          <td> 8.1</td>
          <td> Blood urea increased</td>
          <td> 8.1</td>
          <td>  Brain oedema</td>
          <td> 8.1</td>
        </tr>
        <tr>
          <th>117908</th>
          <td>      Coma</td>
          <td> 8.1</td>
          <td>                  Diabetes mellitus</td>
          <td> 8.1</td>
          <td>                      Gastroenteritis</td>
          <td> 8.1</td>
          <td>       Hyperglycaemia</td>
          <td> 8.1</td>
          <td> Hyponatraemia</td>
          <td> 8.1</td>
        </tr>
        <tr>
          <th>117908</th>
          <td> Infection</td>
          <td> 8.1</td>
          <td>                            Ketosis</td>
          <td> 8.1</td>
          <td>                             Vomiting</td>
          <td> 8.1</td>
          <td>     Weight decreased</td>
          <td> 8.1</td>
          <td>           NaN</td>
          <td> NaN</td>
        </tr>
      </tbody>
    </table>
    <p>3 rows × 10 columns</p>
    </div>



.. code:: python

    flu_vaxxers_idx = vax[vax.VAX_TYPE.str.contains("FLU")].index
    flu_vaxxers = data[data.index.isin(flu_vaxxers.index)]
    non_flu_vaxxers = data[~data.index.isin(flu_vaxxers.index)]
    print(len(flu_vaxxers), len(non_flu_vaxxers))

.. parsed-literal::

    1700 10549


.. code:: python

    flu_vaxxers.AGE_YRS.mean()



.. parsed-literal::

    47.675095541401276



.. code:: python

    non_flu_vaxxers.AGE_YRS.mean()



.. parsed-literal::

    17.280617424634912



.. code:: python

    print(len(non_flu_vaxxers[non_flu_vaxxers.AGE_YRS < 20][non_flu_vaxxers.DIED == "Y"]))
    print(len(non_flu_vaxxers[non_flu_vaxxers.AGE_YRS < 20]))

.. parsed-literal::

    109
    6372


.. code:: python

    print(len(flu_vaxxers[flu_vaxxers.AGE_YRS < 20][flu_vaxxers.DIED == 'Y']))
    print(len(flu_vaxxers[flu_vaxxers.AGE_YRS < 20]))

.. parsed-literal::

    3
    132


.. code:: python

    from scipy import stats
    oddsratio, pvalue = stats.fisher_exact([[109, 6372], [3, 132]])
.. code:: python

    pvalue



.. parsed-literal::

    0.49887148141449822



.. code:: python

    oddsratio



.. parsed-literal::

    0.75266792215944756



.. code:: python

    a = len(non_flu_vaxxers[non_flu_vaxxers.DIED == "Y"])
    b = len(non_flu_vaxxers)
    c = len(flu_vaxxers[flu_vaxxers.DIED == "Y"])
    d = len(flu_vaxxers)
    oddsratio, pvalue = stats.fisher_exact([[a, b], [c, d]])
    print(oddsratio, pvalue)

.. parsed-literal::

    1.37516984232 0.274115058908


.. code:: python

    df = data.copy()
    # data without age is unusable
    df = data.dropna(subset=["AGE_YRS"])
    
    vaxes = set(vax.VAX_TYPE)
    #vaxes = ['HBHEPB']
    
    for vtype in vaxes:
        vaxxers_idx = vax[vax.VAX_TYPE == vtype].index
        vaxxers = df[df.index.isin(vaxxers_idx)]
        non_vaxxers = df[~df.index.isin(vaxxers_idx)]
        a = len(vaxxers[vaxxers.DIED == "Y"])
        b = len(vaxxers[vaxxers.DIED != "Y"])
        c = len(non_vaxxers[non_vaxxers.DIED == "Y"])
        d = len(non_vaxxers[non_vaxxers.DIED != "Y"])
        oddsratio, pvalue = stats.fisher_exact([[a, b], [c, d]])
        print()
        print(vtype, pvalue, oddsratio)
        print(a, b, c, d, a + b + c + d)
        print(vaxxers.AGE_YRS.mean(), non_vaxxers.AGE_YRS.mean())    

.. parsed-literal::

    
    RAB 0.640975771751 0.0
    0 103 139 10981 11223
    32.4165048544 21.4317266187
    
    MEN 1.0 0.0
    0 54 139 11030 11223
    28.2814814815 21.4999104665
    
    OPV 1.0 0.960627537837
    13 1075 126 10009 11223
    3.59761029412 23.4578687716
    
    ANTH 0.000938474717767 0.0
    0 613 139 10471 11223
    34.9450244698 20.7576248822
    
    DTPPHIB 1.0 0.0
    0 1 139 11083 11223
    1.3 21.5343432543
    
    TYP 0.666088535285 1.32267599686
    2 121 137 10963 11223
    36.6894308943 21.3645855856
    
    LYME 0.443113623489 0.502367015695
    2 313 137 10771 11223
    48.6844444444 20.7484506784
    
    TTOX 0.407534749077 0.0
    0 114 139 10970 11223
    40.1403508772 21.3415879017
    
    TD 2.23805753924e-06 0.0
    0 1047 139 10037 11223
    33.8450811843 20.2657134434
    
    CHOL 1.0 0.0
    0 4 139 11080 11223
    29.8 21.5295926553
    
    DTPIPV 1.0 0.0
    0 1 139 11083 11223
    0.5 21.5344145429
    
    HEP 4.88786873265e-06 2.35364259029
    51 2190 88 8894 11223
    15.3066041946 23.0859051436
    
    HEPA 0.0347329423868 0.0
    0 307 139 10777 11223
    32.435504886 21.2259069256
    
    HBHEPB 6.15267741629e-12 7.67676181261
    22 265 117 10819 11223
    0.826829268293 22.0759326993
    
    PPV 0.734238451026 1.0773526715
    10 744 129 10340 11223
    56.1737400531 19.0376062661
    
    YF 0.183401594289 2.63802800048
    2 61 137 11023 11223
    40.2619047619 21.4268100358
    
    DTAP 1.07879583651e-11 3.38803088803
    65 2282 74 8802 11223
    1.83838943332 26.7400856242
    
    DTP 0.195309876072 1.93212508884
    5 210 134 10874 11223
    2.23023255814 21.9095385174
    
    HIBV 2.86137260249e-09 3.15884871749
    48 1586 91 9498 11223
    1.14547123623 25.0065700282
    
    UNK 1.0 0.0
    0 60 139 11024 11223
    28.54 21.4948759294
    
    HBPV 1.0 0.0
    0 8 139 11076 11223
    0.5875 21.5474810522
    
    FLU3 0.217755367723 0.685820051414
    14 1556 125 9528 11223
    47.6750955414 17.2806174246
    
    MU 1.0 0.0
    0 1 139 11083 11223
    11.0 21.5334788808
    
    MER 1.0 0.0
    0 1 139 11083 11223
    3.0 21.5341917662
    
    IPV 4.14195375139e-25 7.44513263263
    59 999 80 10085 11223
    2.23988657845 23.5405705853
    
    MEA 0.24943068608 3.64361001318
    1 22 138 11062 11223
    23.9086956522 21.5276607143
    
    RV 0.526161977282 1.21102965135
    7 465 132 10619 11223
    0.577118644068 22.4525439494
    
    PLAGUE 1.0 0.0
    0 1 139 11083 11223
    20.0 21.5326768847
    
    DT 0.567198368149 1.20970575318
    1 66 138 11018 11223
    18.6567164179 21.5498117605
    
    BCG 1.0 0.0
    0 1 139 11083 11223
    56.5 21.529424345
    
    DTPHIB 0.0530225135638 2.95595959596
    4 110 135 10974 11223
    1.44473684211 21.7386803493
    
    JEV 0.239999377577 3.81746031746
    1 21 138 11063 11223
    33.2363636364 21.5095527185
    
    SMALL 1.0 0.0
    0 3 139 11081 11223
    21.1333333333 21.5326470588
    
    RUB 1.0 0.0
    0 22 139 11062 11223
    40.6363636364 21.4950183019
    
    DTAPH 1.0 0.0
    0 3 139 11081 11223
    1.23333333333 21.5379679144
    
    MMR 0.00113556919612 0.391761221163
    11 1994 128 9090 11223
    7.4536159601 24.5948361901
    
    VARCEL 1.31017368942e-06 0.247988679365
    9 2419 130 8665 11223
    7.67471169687 25.3582148948


.. code:: python

    # data is expected global
    def test_vt(vt, age_min=0, age_max=100):
        df = data[data.AGE_YRS >= age_min][data.AGE_YRS <= age_max]
        vaxxers_idx = vax[vax.VAX_TYPE == vt].index
        vaxxers = df[df.index.isin(vaxxers_idx)]
        non_vaxxers = df[~df.index.isin(vaxxers_idx)]
        a = len(vaxxers[vaxxers.DIED == "Y"])
        b = len(vaxxers[vaxxers.DIED != "Y"])
        c = len(non_vaxxers[non_vaxxers.DIED == "Y"])
        d = len(non_vaxxers[non_vaxxers.DIED != "Y"])
        oddsratio, pvalue = stats.fisher_exact([[a, b], [c, d]])
        print()
        print(len(vaxxers), len(non_vaxxers))
        print(vt, pvalue, oddsratio)
        print(a, b, c, d, a + b + c + d)
        print(vaxxers.AGE_YRS.mean(), non_vaxxers.AGE_YRS.mean())
        return vaxxers, non_vaxxers
    hbhepb, non_hbhepb = test_vt('HBHEPB')

.. parsed-literal::

    
    287 10936
    HBHEPB 6.15267741629e-12 7.67676181261
    22 265 117 10819 11223
    0.826829268293 22.0759326993


.. code:: python

    hbhepb, non_hbhepb = test_vt('HBHEPB', 0.3, 0.3)

.. parsed-literal::

    
    28 216
    HBHEPB 0.119009355923 3.12
    3 25 8 208 244
    0.3 0.3


.. code:: python

    hep, non_hep = test_vt('HEP', 0.3, 0.3)

.. parsed-literal::

    
    30 214
    HEP 0.0333272009241 4.54945054945
    4 26 7 207 244
    0.3 0.3


.. code:: python

    vax[vax.VAX_TYPE == 'HBHEPB'].index



.. parsed-literal::

    Int64Index([117883, 117884, 117891, 118186, 118312, 118462, 118465, 118466, 118499, 118518, 118646, 118660, 118672, 118735, 118787, 118802, 118836, 118839, 118902, 118916, 118928, 119176, 119251, 119446, 119737, 119764, 119799, 120473, 120567, 120812, 120850, 120985, 121000, 121028, 121059, 121068, 121110, 121158, 121235, 121259, 121335, 121427, 121435, 121500, 121525, 121554, 121571, 121609, 121699, 121701, 121792, 121808, 121810, 121855, 121859, 121864, 121865, 121890, 121898, 121922, 121928, 121975, 121993, 122057, 122071, 122138, 122144, 122145, 122159, 122160, 122254, 122410, 122671, 122712, 123001, 123172, 123176, 123191, 123202, 123241, 123251, 123252, 123264, 123316, 123317, 123340, 123342, 123370, 123886, 124129, 124135, 124220, 124739, 124774, 124785, 124961, 125011, 125012, 125114, 125127, ...], dtype='int64')



.. code:: python

    vax[vax.VAX_TYPE == 'HEP'].index



.. parsed-literal::

    Int64Index([117875, 117876, 117880, 117882, 117897, 117905, 117911, 117915, 117918, 117919, 117921, 117924, 117929, 117941, 117942, 117944, 117945, 117946, 117954, 117955, 117966, 117973, 117974, 117976, 117978, 117983, 117987, 117991, 117992, 118004, 118007, 118008, 118019, 118025, 118026, 118028, 118051, 118055, 118079, 118083, 118112, 118117, 118124, 118130, 118139, 118140, 118144, 118145, 118147, 118149, 118151, 118152, 118153, 118155, 118156, 118157, 118159, 118162, 118173, 118176, 118177, 118179, 118182, 118207, 118208, 118209, 118213, 118216, 118229, 118230, 118238, 118240, 118242, 118243, 118244, 118246, 118250, 118251, 118272, 118280, 118281, 118283, 118286, 118303, 118304, 118306, 118318, 118321, 118322, 118323, 118324, 118326, 118331, 118334, 118336, 118386, 118387, 118388, 118389, 118390, ...], dtype='int64')



.. code:: python

    set(vax[vax.VAX_TYPE == 'HEP'].index).intersection(set(vax[vax.VAX_TYPE == 'HBHEPB'].index))



.. parsed-literal::

    {118928, 121864, 127355, 127356, 127357, 127358, 127359, 127360, 127361}



.. code:: python

    print(vax.loc[118928])
    print(vax.loc[121864])

.. parsed-literal::

             VAX_TYPE                VAX_MANU  VAX_LOT  VAX_DOSE VAX_ROUTE  \
    VAERS_ID                                                                 
    118928       DTAP  CONNAUGHT LABORATORIES  0925880       NaN        IM   
    118928     HBHEPB        MERCK & CO. INC.    0327H       NaN        IM   
    118928        HEP        MERCK & CO. INC.    1478H       NaN        IM   
    118928         TD  CONNAUGHT LABORATORIES  0967100       NaN        IM   
    
             VAX_SITE                     VAX_NAME  
    VAERS_ID                                        
    118928         LL              DTAP (TRIPEDIA)  
    118928         RL         HIB + HEP B (COMVAX)  
    118928         RA              HEP B (FOREIGN)  
    118928         LA  TD ADSORBED (NO BRAND NAME)  
    
    [4 rows x 7 columns]
             VAX_TYPE          VAX_MANU VAX_LOT  VAX_DOSE VAX_ROUTE VAX_SITE  \
    VAERS_ID                                                                   
    121864     HBHEPB  MERCK & CO. INC.     NaN       NaN       NaN      NaN   
    121864        HEP  MERCK & CO. INC.     NaN       NaN       NaN      NaN   
    
                           VAX_NAME  
    VAERS_ID                         
    121864     HIB + HEP B (COMVAX)  
    121864    HEP B (RECOMBIVAX HB)  
    
    [2 rows x 7 columns]


.. code:: python

    hep.index



.. parsed-literal::

    Int64Index([118388, 119266, 119826, 120420, 120482, 120891, 120901, 121007, 121151, 122391, 123424, 124763, 125099, 125585, 125713, 126044, 126077, 126344, 126363, 126992, 127161, 127408, 127878, 128119, 129571, 129871, 131398, 131432, 131547, 132806], dtype='int64')



.. code:: python

    hbhepb.index



.. parsed-literal::

    Int64Index([118186, 118660, 118836, 118902, 119737, 122159, 123317, 125458, 125780, 126438, 127409, 127717, 127744, 127757, 127847, 128069, 128248, 128379, 128659, 129456, 129513, 129955, 130324, 130767, 132108, 132636, 131737, 132966], dtype='int64')



.. code:: python

    # now we need to test a list of VAX_TYPE
    
    # data is expected global - from first cell.
    def test_vts(vts, age_min=0, age_max=100):
        """
        Take a list of VAX_TYPE.
        Test the list against those not in the list for death odds.
        """
        df = data[data.AGE_YRS >= age_min][data.AGE_YRS <= age_max]
        
        vax_vaxxers = vax[vax.VAX_TYPE.isin(vts)]
    
        vaxxers_idx = vax_vaxxers.index
        vaxxers = df[df.index.isin(vaxxers_idx)]
        non_vaxxers = df[~df.index.isin(vaxxers_idx)]
        a = len(vaxxers[vaxxers.DIED == "Y"])
        b = len(vaxxers[vaxxers.DIED != "Y"])
        c = len(non_vaxxers[non_vaxxers.DIED == "Y"])
        d = len(non_vaxxers[non_vaxxers.DIED != "Y"])
        oddsratio, pvalue = stats.fisher_exact([[a, b], [c, d]])
        print()
        print(len(vaxxers), len(non_vaxxers))
        print(vts, pvalue, oddsratio)
        print(a, b, c, d, a + b + c + d)
        print(vaxxers.AGE_YRS.mean(), non_vaxxers.AGE_YRS.mean())
        return vaxxers, non_vaxxers
    hbhepb, non_hbhepb = test_vts(['HBHEPB', 'HEP'], 0.3, 0.3)

.. parsed-literal::

    
    58 186
    ['HBHEPB', 'HEP'] 0.00459973660781 6.24509803922
    7 51 4 182 244
    0.3 0.3


.. code:: python

    hbhepb, non_hbhepb = test_vts(['HBHEPB', 'HEP'], 0.3, 0.5)

.. parsed-literal::

    
    190 436
    ['HBHEPB', 'HEP'] 8.30684615678e-05 5.25722543353
    17 173 8 428 626
    0.415789473684 0.383944954128


.. code:: python

    hbhepb, non_hbhepb = test_vts(['HBHEPB', 'HEP'], 0, 1)

.. parsed-literal::

    
    738 1349
    ['HBHEPB', 'HEP'] 1.33118704219e-11 4.4798643493
    64 674 28 1321 2087
    0.361924119241 0.604447739066


.. code:: python

    dtp, non_dtp = test_vts(['DTAP', 'DTP'], 0.3, 0.3)

.. parsed-literal::

    
    204 40
    ['DTAP', 'DTP'] 1.0 2.01030927835
    10 194 1 39 244
    0.3 0.3


