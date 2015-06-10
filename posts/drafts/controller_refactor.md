---
title: 'Creating dojoCMS Part 8 - Adding has_many / belongs_to relationship'
date: '2015-06-02'
description:
tags: []
---

  def create
    user = User.find(params[:user_id])
    blocked_user = User.find(params[:blocked_user])
    if user.relationships.find_by_other_user_id(params[:blocked_user])
      user.relatiotnships
    else
      user.relatiotnships.create({:status => "blocked", :other_user_id => params[:blocked_user]})
    end
      flash[:success] = "You have successfully blocked #{blocked_user.steam_name}"
      redirect_to :root
  end

  vs 


  def self.create_blocked_relationship(user, blocked_user)
    relationship = Relationship.find_by_user_id_and_other_user_id(user.id, blocked_user.id)
    if relationship.present?
      relationship.status = "blocked"
      relationship.save
      return relationship
    else 
      new({user_id: user.id, other_user_id: blocked_user.id, status: "blocked"})
    end
  end

