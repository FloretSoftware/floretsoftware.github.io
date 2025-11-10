---
title: Goblin with a Gun
layout: post
summary: An endless wave based top-down arena shooter with dynamic stats and a boss
  fight!
author: floretdev
date: '2024-03-01 17:00:00 +0000'
category: portfolio
thumbnail: "/assets/img/posts/goblinwithagun.png"
keywords: unity, goblin, with , a , gun, portfolio, gamedev
permalink: "/blog/goblin-with-a-gun/"
usemathjax: true
---

> **Game Engine/Language**: Unity / C#

> **Role**: Solo Dev

> **Duration of Work**: 8 Weeks

> **End Of Project**: 1st March 2024

>**Github Repository**: [Click Here!](https://github.com/Transference-OperatorHaven/CSharp-Uni-Game)
 

**Game Page** :
<iframe height="167" frameborder="0" src="https://itch.io/embed/2558100" width="552"><a href="https://floretsoftware.itch.io/goblin-with-a-gun">Goblin with a Gun by Floret Software</a></iframe>

This was a solo project I made for a university module. It is a feature complete endless top down shooter with dynamic stats, guns and even a boss fight every ten waves. I'm super proud of this game.

The videos below showcase the gameplay as well as the variety of guns featured in the game.

<iframe width="560" height="315" src="https://www.youtube.com/embed/LrFkhAKxbik?si=B6mjQnuLYAsmbfc_" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe> <iframe width="560" height="315" src="https://www.youtube.com/embed/3_JKxw2B0TA?si=RniJPFtoqkWy_nrF" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Below is a code snippet of how dynamic powerup attributes are handled in a way that creates clean processes
```

    void TriggerDeath()
    {
        OnPlayerDeath?.Invoke();
        Camera.main.enabled = false;
        SceneManager.LoadScene(currentScene.name, LoadSceneMode.Single);
    }

    public void UpdateDodgeStats()
    { 

        dodgeCooldownLengthCurrent = dodgeCooldownLengthBase * (1 - dodgeCooldownLengthModifier);
        dodgeVelocityCurrent = dodgeVelocityBase * (1 + dodgeVelocityModifier);

    }

    public void UpdateGunStats()
    {
        gunDamageCurrent = gunDamageBase * (1 + gunDamageModifier);
        gunSpeedCurrent = gunSpeedBase * (1 + gunSpeedModifier);
        gunFireRateCurrent = gunFireRateBase * (1 + gunFireRateModifier);
        gunLifetimeCurrent = gunLifetimeBase * (1 + gunLifetimeModifier);
        reloadTimeCurrent = reloadTimeBase * (1 + reloadTimeModifier);
        gunMagCurrent = gunMagBase * (1 + gunMagModifier);
        specialReloadRoundsCutOff = gunMagBase * 0.875f;
    }

    public void UpdateSwordStats()
    {
        swordRadiusCurrent = swordRadiusBase * (1 + swordRadiusModifier);
        swordDurationCurrent = swordDurationBase * (1 + swordDurationModifier);
        swordCooldownLengthCurrent = swordCooldownLengthBase * (1 + swordCooldownLengthModifier);
        swordDamageCurrent = swordDamageBase * (1 + swordDamageModifier);
    }
```

Below is a code snippet of the dynamic powerup system's dynamic colour particle effects.

```
 void CalculateParticleColorAndApply()
    {
        particleColor.r = allColors.x / numberOfBuffs;
        particleColor.g = allColors.y / numberOfBuffs;
        particleColor.b = allColors.z/ numberOfBuffs;
        particleColor.a = 255;
        psMain.startColor = particleColor;
    }

    public void SetParticleColor(Color color)
    {
        numberOfBuffs += 1;
        if(numberOfBuffs > 0)
        {
            ps.Play(true);
        }
        allColors += new Vector4 (color.r,color.g,color.b,color.a);
        CalculateParticleColorAndApply();

    }

    public void RemoveColor(Color color)
    {
        numberOfBuffs -= 1;
        if(numberOfBuffs <= 0)
        {
            ps.Stop(true ,ParticleSystemStopBehavior.StopEmittingAndClear);
        }
        allColors -= new Vector4(color.r, color.g, color.b, color.a);
        CalculateParticleColorAndApply();

    }
```
