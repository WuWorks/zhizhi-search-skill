[English](README_EN.md) | 中文

# 知止 · zhizhi-search

**Knowing when to stop — Intent-bounded, minimally sufficient search.**

## 介绍

知止是一个检索检查点的 skill。模型在替代用户联网搜索时，会在每一轮搜索之后停下来判一次：搜索所得到的，是否为用户真正需要的东西。

## 设计的初衷

模型在联网检索时通常会出现隐蔽性行为：它会在中途换掉搜索对象，过度替换关键词，却不告诉用户，我叫它为隐蔽性的伪欺骗行为。

> 伪欺骗在项目中的解释：是一种非携带欺骗的目的，却行为上与目的发生歧义的行为。

举例：把你的词换成更常见的近义说法，挑一个名字相同、说的却不是同一件事的东西顶上，或者顺着结果里的话题越走越远。最后交出的答案有出处、有结论、看上去完整，答的却是另一个问题。

错不在字面——每个字都认识，只是对象换了，所以很难当场发现。

## 它解决什么

这个 skill 只做三件事。

- **贴合需求**：它保证最后答的，是你问的那件事。
- **减少漂移**：它能在中途发现偏了，然后停下，不拿搜到的东西凑一个答案。
- **承认结果**：它敢说查不到，不把「没找到」包装成「它大概想问的是另一个词」。

三件事做成了，你会直接看到其中一种：它继续往下搜，最后答的还是你原来问的那件；它停下来，告诉你搜到的东西不是你要的；它直接说，没查到。

它不教模型怎么搜索——只在每轮搜索之后判一次方向。

顺带还省时间、省 token：方向错了就停，不把一个坏起点滚成十轮无效搜索。token 这一项目效果仍是实验性的。

## “知止”什么时候触发

使用所在Agent指定的技能触发字符或发送“使用zhizhi-search技能”即可使用

举例：从网上拿一个具体答案、而这个答案存在对错时——查资料、找东西、核事实、比对出处都算。

纯聊天、纯推理、写作、已有材料足够回答时，它不启动。

## 怎么安装（所有Agent均可使用）

1.把 `SKILL.md` 放进 skills 目录：

```markdown
~/.agent/skills/zhizhi-search/SKILL.md
~/.codex/skills/zhizhi-search/SKILL.md
~/.claude/skills/zhizhi-search/SKILL.md
......
```

2.把`SKILL.md` 拖动给你的Agent代理，它会自动安装。

3.或者用一条命令装：

```sh
npx skills add WuWorks/zhizhi-search-skill          # 安装
npx skills add WuWorks/zhizhi-search-skill --list   # 只看会装什么
```

## 兼容性

任何支持 `skills/` 目录加载的 Agent 都能用，包括 Claude Code、Codex、DSH 等。技能目录名统一为 `zhizhi-search`。

## 许可证

[MIT](LICENSE)。可以自由使用、修改、分发，保留版权声明即可。

